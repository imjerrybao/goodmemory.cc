---
title: 爬虫(spider/crawl)原理
author: admin
layout: post
date: 2015-10-26
url: /爬虫spidercrawl原理/
categories:
  - 爬虫研究

---
学习了很多爬虫的原理和模块划分后，发现很多项目的原理以及组件划分似乎都是类似的，所以虽然这篇文章的原名不是介绍爬虫原理，但内容时机上就是介绍通用爬虫的基本原理和流程以及工作组件划分 &#8211; [SpiderDuck：Twitter的实时URL抓取器][1]
  
英文原文已经被twitter移除了，大家且看且珍惜吧。

正文：

推文中常常含有指向 web 各种内容的链接，包括图像、视频、新闻文章以及博客帖。SpiderDuck 是Twitter 的一项用于对这些链接进行实时抓取、解析下载内容并提取有趣的元数据的服务，并且，它使得其它的 Twitter 服务能够在数秒钟内即可使用这些数据。

Twitter 的许多的团队都需要访问链接的内容，尤其是需要用实时内容来改进 Twitter 的产品。比如：
  
搜索：需要对解析后的 URL 建立索引并改进搜索质量；
  
客户端：需要在推文旁边同时显示某些类型的媒体内容，比如照片；
  
发推按钮：用以统计每条 URL 到底被共享了多少次；
  
信任与安全部门：用以帮助检测恶意软件和垃圾信息；
  
分析：发掘关于 Twitter 上被共享的链接的统计汇总信息。
  
背景

SpiderDuck 出现之前，Twitter 有一个用发送 HEAD 请求和跟踪跳转来解析所有推文中的 URL 的服务。这个服务很简单，也满足了公司当时的需求，但是它有几项限制：
  
它解析 URL，但是并不真正的下载内容。解析信息被存在内存中缓存里但是并没有永久地保存在磁盘上。这意味着如果内存中的缓存实例被重启的话，数据就都会丢失。
  
它没有实现现代抓取机器人的“礼貌性”，比如访问频率限制和遵守 robots.txt 的指示等等。
  
显然，我们需要建造一个能够克服上述限制并满足公司的长远目标的真正的 URL 抓取器。我们最初的想法使用某个开源的抓取代码，或以其为基础，但是我们意识到几所有能用的开源抓取器都有两个我们不需要的特征：
  
它们都是递归抓取器。也就是说，它们是被设计来抓取页面并递归抓取从页面里面提取出来的所有链接的。递归抓取给爬虫的调度和长期队列的维护带来了很多复杂性，在我们情况下并不必要。
  
它们被优化来进行大批量抓取。我们需要的是快速的、实时的 URL 抓取。
  
因此，我们决定设计一个能够满足 Twitter 的实时需要的新系统，并能够随其增长水平扩展。为了避免重新发明轮子，我们把新系统大部分建立在了开源的模块之上，从而可以继续利用开源社区的贡献。

这是 Twitter 的工程问题里面很典型的一个——它们和其它大型互联网公司的问题很类似，但是要求所有东西都能够实时工作又带来了独特而有趣的挑战。

系统概览

这里是讲述 SpiderDuck 如何工作的概览。下图画出了它的主要部件。

[SpiderDuck：Twitter的实时URL抓取器][2]
  
Kestrel：这是一个在 Twitter 广泛使用的，用以对新进推文进行排队的消息队列系统。

Scheduler：这些工作单元决定是否要抓取一个 URL，计划抓取时间，并跟踪重定向跳转（如果有的话）。抓取之后，它会解析下载的内容，提取元数据（metadata），并把元数据写回 Metadata Store，把原始数据写入 Content Store。每个 scheduler 都独立工作；也就是说，我们可以把任意数量的 scheduler 加入到系统中，随推文和 URL 的数量增加水平地扩展系统。

Fetcher：这些是用于维护短期 URL 抓取队列的 Thrift 服务器，它们发送实际的 HTTP 抓取请求并实现速率控制和处理 robots.txt。就像 scheduler 一样，它们可以随抓取速率水平扩展。

Memcached：这是 fetcher 使用的分布式缓存，用以临时存储 robots.txt 文件。

Metadata Store：这是一个基于 Cassandra 的分布式散列表，用以存储网页的元数据和以 URL 索引的解析信息，以及系统最近遇到的每个 URL 的抓取状态。这个存储为 Twitter 所有的需要实时访问 URL 数据的客户服务。

Content Store：这是一个 HDFS 集群，用以存储下载的内容和所有的抓取信息。

现在我们将更详细地介绍 SpiderDuck 的两个主要部件——URL Scheduler 和 URL Fetcher。

[URL Scheduler-URL 调度器][3])

下面的图表画出了 SpiderDuck Scheduler 里面的几个处理阶段。
  
SpiderDuck：Twitter的实时URL抓取器
  
就像 SpiderDuck 的大部分一样，Scheduler 也是建立在一个 Twitter 开发的开叫做 Finagle 的开源异步 RPC 框架之上。（实际上，这是最早的一个利用 Finagle 的项目）。上图里面的每一个方块，除了 Kestrel Reader，都是一个 Finagle Filter —— 一个允许把一系列处理阶段连接成一个完全异步流水线的抽象概念。完全异步则允许 SpiderDuck 以较少的、固定数量的线程处理很高的流量。

Kestrel Reader 会不断地询问是否有新的推文出现。当推文进来时，它们被发送到 Tweet Processor，它从其中提取 URL。每条 URL 然后就会被送到 Crawl Decider 阶段。该阶段从 Metadata Store 读取 URL 的抓取状态，以确定 SpiderDuck 是否之前已经见过了这个 URL。Crawl Decider 然后根据一个预先制定的抓取策略（就是如果 SpiderDuck 在过去 X 天内已经见过了此 URL 则不再重复抓取）来决定是否该 URL 应该被抓取。如果 Decider 决定不抓取该 URL，它会记录状态以表示处理完成。如果它决定要抓取这个 URL，它就会把 URL 送到 Fetcher Client 阶段。

Fetcher Client 阶段使用客户端库和 Fetcher 交谈。客户端库实现了逻辑用以够决定哪个 Fetcher 会被用来抓取该 URL；它也能够处理重定向跳转。（重定向跳转链非常普遍，因为 Twitter 上的贴的 URL 多数都被缩短了）经过 Scheduler 的每个 URL 都有一个相关的上下文对象。Fetcher Client 会把包括状态、下载的头以及内容的抓取信息添加到上下文对象中，并将其传递给 Post Processor。Post Processor 把下载的数据交给元数据提取器，它会检测页面的编码，并使用一个开源的 HTML5 解析器解析页面的内容。提取库实现了一系列启发式算法，用于提取诸如标题、简介、以及代表图片等元数据。Post Processor 然后把所有的元数据和抓取信息写入 Metadata Store。如果需要的话，Post Processor 还会调度一系列相关抓取。相关抓取的例子之一就是嵌入的媒体内容，比如图片。

后期处理（post processing）结束之后，URL 上下文对象被交给下一个阶段，其会使用一个叫做 Scribe 的开源日志聚集器在 Content Store （HDFS）的日志中记录所有信息，包括完整的内容。该阶段还通知所有的感兴趣的监听者 URL 处理结束了。通知使用了一个简单的发布者-订阅者模型，用 Kestrel 的分散队列实现。

所有的处理阶段都是异步运行的 —— 没有任何线程会等待一个阶段完成。和每个正在处理中的 URL 相关的状态都保存在相关的上下文对象中，所以线程模型也非常简单。异步实现也受益于 Finagle 和 Twitter Util 库提供的方便的抽象和构件。

[URL Fetcher-URL 抓取器][2]

让我们来看看 Fetcher 如何处理一条 URL。
  
SpiderDuck：Twitter的实时URL抓取器
  
Fetcher 通过 Thrift 界面接收到 URL。经过一些简单的确认之后，Thrift 处理器把 URL 传递给 Request Queue Manager （请求队列管理器），其把 URL 指定给某个合适的请求队列。一个调度了的任务会按照固定的速率从请求队列中读取。一旦 URL 被从队列中取出来了，它就会被送到 HTTP Service 处理。建造在 Finagle 上面的 HTTP Service 首先检查 URL 相关的主机是否已经在缓存中了。如果没有，那么它会为它创建一个 Finagle 客户，并调度好 robots.txt 文件的抓取。在 robots.txt 被下载之后，HTTP Service 会抓取许可的 URL。robots.txt 文件本身是被缓存的，在进程中的 Host Cache 和 Memcached 里面各一份，以防止每次有该主机新的 URL 进来时重复抓取。

一些叫做 Vulture （秃鹫）的任务周期性地检查 Request Queue （请求队列）和 Host Cache （主机缓存）以寻找有一段时间都没有被使用的队列和主机；如果找到了，它们就会被删除。Vulture 还会通过日志和 Twitter Commons 状态输出库报告有用的统计信息。

Fetcher 的 Request Queue 还有一个重要的目标：速率限制。SpiderDuck 限制对每个域名发出的 HTTP 抓取请求，以保证不会使得 web 服务器过载。为了准确地限制速率，SpiderDuck 保证每一个 Request Queue 在任一时刻都被指定到刚好一个 Fetcher，并且能够在 Fetcher 失效的时候自动重新指定到另一个 Fetcher 上。一个叫做 Pacemaker 的机群软件包会把 Request Queue 指定给 Fetcher 并管理失效转移。Fetcher 客户库根据 URL 的域名把它们分配到不同的 Request Queue。对于整个 web 设置的默认速率限制也能够根据需要被对于具体的域名设置的速率限制取代。也就是说，如果 URL 进来的速度比处理它们的速度还要快，它们就会拒绝请求，以告诉客户端应该收敛，或者采取其它合适措施。

为了安全，Fetcher 被部署到了 Twitter 数据中心里面的一个特殊区域 DMZ。这意味着 Fetcher 不能访问 Twitter 的产品机群和服务。所以，确保它们的轻量级设计和自力更生非常重要，这也是一条指导很多方面的设计的原则。

Twitter 如何使用 SpiderDuck

Twitter 服务以很多方式使用 SpiderDuck 的数据。大部分会直接查询 Metadata Store 以获取 URL 的元数据（比如，标题）以及解析信息（所有重定向跳转之后的最终规范化 URL）。Metadata Store 是实时填充的，一般是在 URL 在推文中发布后的几秒钟内。这些服务并不直接和 Cassandra 交谈，而是通过一个代理这些请求的 Spiderduck Thrift 服务器。这个中间层为 SpiderDuck 提供了灵活性，使其能够透明地切换存储系统，如有需有。它同时也支持了比直接访问 Cassandra 更高级的 API 抽象。

其它服务会周期性的处理 SpiderDuck 在 HDFS 上的日志以生成聚合统计信息，用以 Twitter 的内部测量仪表板或者进行其它批量分析。仪表板帮助我们回答诸如“每天 Twitter 上有多少图片被共享？”、“Twitter 用户最经常链接到什么新闻网站？”以及“我们昨天从某个网站抓取了多少网页？”之类的问题。

需要注意的是，这些服务一般不会告诉 SpiderDuck 需要抓取什么东西；SpiderDuck 已经抓取了进入 Twitter 的所有 URL。取而代之，这些服务在 URL 可用之后询问它们的相关信息。SpiderDuck 也允许这些服务直接请求 Fetcher 通过 HTTP 抓取任意内容，（这样它们就能受益于我们的数据中心设置、速率限制、robot.txt 支持等功能），但这种用法并不普遍。

性能数据

SpiderDuck 每秒处理数百条 URL。这中间的大部分都是在 SpiderDuck 的抓取策略所定义的时间窗口里独一无二（unique）的，所以它们会被抓取。对于抓取了的 URL，SpiderDuck 处理延迟中值在 2 秒以下，99% 的处理延迟低于 5 秒。该延迟是基于推问发布时间测量的，也就是说在用户点击“发推”按钮后 5 秒内，推文中的 URL 就被提取出来，做好了抓取准备，获取了所有的重定向跳转，下载并解析了内容，并提取了元数据，并且它们已经通过 Metadata Store 对于客户可用了。这中间大部分的时间要么花在了 Fetcher Request Queue （因为速率限制）中，或者花在了从外部 web 服务器实际获取该 URL 上。SpiderDuck 本身只增加了几百毫秒的额外处理时间，大部分都花在 HTML 解析上。

SpiderDuck 的基于 Cassandra 的 Metadata Store 能够处理接近每秒 10,000 个请求。这些请求一般是针对单独或者小批次（小于 20 个）URL 的，但是它也能够处理大批次（200~300 个 URL）的请求。这个存储系统的读取延迟中值在 4 ~ 5 秒左右，第 99 百分区间在 50 ~ 60 毫秒左右。

致谢

SpiderDuck 的核心团队包括以下成员：Abhi Khune，Michael Busch，Paul Burstein，Raghavendra Prabhu，Tian Wang 以及 Yi Zhuang。此外，我们希望对遍布全公司的以下人员表示感谢，他们要么直接为该项目做出了贡献，帮助设置了 SpiderDuck 直接依赖的部件（比如 Cassandra、Finagle、Pacemaker 以及 Scribe），要么帮助建立了 SpiderDuck 独特的数据中心设置： Alan Liang, Brady Catherman, Chris Goffinet, Dmitriy Ryaboy, Gilad Mishne, John Corwin, John Sirois, Jonathan Boulle, Jonathan Reichhold, Marius Eriksen, Nick Kallen, Ryan King, Samuel Luckenbill, Steve Jiang, Stu Hood and Travis Crawford。我们也要感谢整个 Twitter 搜索团队提供的宝贵的设计反馈和支持。如果你也想参与这样的项目，和我们一起飞吧！

原文地址：http://engineering.twitter.com/2011/11/spiderduck-twitters-real-time-url.htmlhttp://engineering.twitter.com/2011/11/spiderduck-twitters-real-time-url.html

2015.10.27补充： &#8211; [爬虫技术浅析][4]

 [1]: http://blog.sina.com.cn/s/blog_72995dcc01011wh4.html
 [2]: http://www.goodmemory.cc/wp-content/uploads/2015/12/SpiderDuck1.jpeg
 [3]: http://www.goodmemory.cc/wp-content/uploads/2015/12/SpiderDuck2.jpeg
 [4]: http://drops.wooyun.org/tips/3915