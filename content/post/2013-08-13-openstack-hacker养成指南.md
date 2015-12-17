---
title: OpenStack Hacker养成指南
author: admin
layout: post
date: 2013-08-12
url: /openstack-hacker养成指南/
duoshuo_thread_id:
  - 6218977950348346113
categories:
  - 开发工具
tags:
  - OpenStack

---
<span style="font-size: 2em;">0 阅读指南</span>

  * 希望本文能够解开你心中萦绕已久的心结，假如是死结，请移步到 <a title="https://wiki.openstack.org/wiki/Main_Page" href="https://wiki.openstack.org/wiki/Main_Page" rel="nofollow">https://wiki.openstack.org/wiki/Main_Page</a>
  * 学习OpenStack其实就是学习各种Python库的过程。
  * 把OpenStack的设计原则贴在你的墙上。 <a title="https://wiki.openstack.org/wiki/BasicDesignTenets" href="https://wiki.openstack.org/wiki/BasicDesignTenets" rel="nofollow">https://wiki.openstack.org/wiki/BasicDesignTenets</a>

# 1 OpenStack Hacker {#openstack_hacker}

<div>
  <ul>
    <li>
      <div>
        态度：开放、主动、沟通
      </div>
    </li>
    
    <li>
      <div>
        影响力：能说、能写、能分享
      </div>
    </li>
    
    <li>
      <div>
        四化：自动化、流程化、系统化、文档化
      </div>
    </li>
  </ul>
  
  <p>
    &nbsp;
  </p>
</div>

# 2 基础技能 {#基础技能}

## Python {#python}

<div>
  <ul>
    <li>
      <div>
        书籍:
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://book.douban.com/subject/5401851/" href="http://book.douban.com/subject/5401851/" rel="nofollow">《python参考手册》</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://book.douban.com/subject/4866934/" href="http://book.douban.com/subject/4866934/" rel="nofollow">《python基础教程》</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        教程: <a title="http://www.codecademy.com/zh/tracks/python" href="http://www.codecademy.com/zh/tracks/python" rel="nofollow">Codecademy</a>
      </div>
    </li>
    
    <li>
      <div>
        挑战: <a title="http://www.pythonchallenge.com/" href="http://www.pythonchallenge.com/" rel="nofollow">Python Challenge</a>
      </div>
    </li>
    
    <li>
      <div>
        文档: <a title="http://docs.python.org/2/index.html" href="http://docs.python.org/2/index.html" rel="nofollow">Python v2.7.3 documentation</a>
      </div>
    </li>
    
    <li>
      <div>
        高阶:
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://docs.python-guide.org/en/latest/" href="http://docs.python-guide.org/en/latest/" rel="nofollow">The Hitchhiker’s Guide to Python!</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://pymotw.com/2/" href="http://pymotw.com/2/" rel="nofollow">Python Module of the Week</a>
          </div>
        </li>
      </ul>
    </li>
  </ul>
</div>

## Linux {#linux}

<div>
  <ul>
    <li>
      <div>
        书籍:
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://vbird.dic.ksu.edu.tw" href="http://vbird.dic.ksu.edu.tw/" rel="nofollow">鸟哥的Linux私房菜</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://book.douban.com/subject/1788421/" href="http://book.douban.com/subject/1788421/" rel="nofollow">《Unix环境高级编程》</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://book.douban.com/subject/1314538/" href="http://book.douban.com/subject/1314538/" rel="nofollow">《UNIX系统编程》</a>
          </div>
        </li>
      </ul>
    </li>
  </ul>
</div>

## Git {#git}

<div>
  <ul>
    <li>
      <div>
        书籍：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://git-scm.com/book/zh" href="http://git-scm.com/book/zh" rel="nofollow">Pro Git</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://www.worldhello.net/gotgithub/index.html" href="http://www.worldhello.net/gotgithub/index.html" rel="nofollow">GotGitHub</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        教程：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://try.github.com/levels/1/challenges/1" href="http://try.github.com/levels/1/challenges/1" rel="nofollow">tryGit</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://gitimmersion.com/lab_01.html" href="http://gitimmersion.com/lab_01.html" rel="nofollow">GitImmersion</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        进阶：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://marklodato.github.com/visual-git-guide/index-zh-cn.html" href="http://marklodato.github.com/visual-git-guide/index-zh-cn.html" rel="nofollow">visual-git-guide</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://nvie.com/posts/a-successful-git-branching-model/" href="http://nvie.com/posts/a-successful-git-branching-model/" rel="nofollow">a-successful-git-branching-model</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        最常用的git命令：<a title="http://www.kernel.org/pub/software/scm/git/docs/everyday.html" href="http://www.kernel.org/pub/software/scm/git/docs/everyday.html" rel="nofollow"> Everyday GIT With 20 Commands Or So</a>
      </div>
    </li>
  </ul>
</div>

## Unittest {#unittest}

<div>
  <ul>
    <li>
      <div>
        教程:<a title="http://docs.python.org/2/library/unittest.html" href="http://docs.python.org/2/library/unittest.html" rel="nofollow"> python unittest</a>
      </div>
    </li>
  </ul>
</div>

# 3 OpenStack 基础 {#openstack_基础}

## The 5-minute Overview {#the_5-minute_overview}

<div>
  <p>
    <strong>OpenStack</strong> is a global collaboration of developers and cloud computing technologists producing the ubiquitous open source cloud computing platform for <em><strong>public and private clouds</strong></em>. The project aims to deliver solutions for all types of clouds by being simple to implement, massively scalable, and feature rich. The technology consists of a series of <a title="https://www.openstack.org/software/" href="https://www.openstack.org/software/" rel="nofollow">interrelated projects</a> delivering various components for a cloud infrastructure solution. <strong>OpenStack</strong>controls <em><strong>large pools of compute, storage, and networking resources</strong></em> throughout a datacenter, all managed through a dashboard that gives administrators control while empowering their users to provision resources through a web interface.
  </p>
  
  <p>
    <a href="http://www.ustack.com/wp-content/uploads/2013/08/11.png"><img alt="1" src="http://www.ustack.com/wp-content/uploads/2013/08/11.png" width="841" height="346" /></a>
  </p>
</div>

## OpenStack 基本概念 {#openstack_基本概念}

<div>
  <ul>
    <li>
      <div>
        介绍： <a title="https://www.openstack.org/software/" href="https://www.openstack.org/software/" rel="nofollow">https://www.openstack.org/software/</a>
      </div>
    </li>
    
    <li>
      <div>
        Compute管理员手册(必看)：<a title="http://docs.openstack.org/trunk/openstack-compute/admin/content/ch_getting-started-with-openstack.html" href="http://docs.openstack.org/trunk/openstack-compute/admin/content/ch_getting-started-with-openstack.html" rel="nofollow">http://docs.openstack.org/trunk/openstack-compute/admin/content/ch_getting-started-with-openstack.html</a>
      </div>
    </li>
    
    <li>
      <div>
        OpenStack End User Guide(必看): <a title="http://docs.openstack.org/user-guide/content/" href="http://docs.openstack.org/user-guide/content/" rel="nofollow">http://docs.openstack.org/user-guide/content/</a>
      </div>
    </li>
    
    <li>
      <div>
        Network管理员手册：<a title="http://docs.openstack.org/folsom/openstack-network/admin/content/" href="http://docs.openstack.org/folsom/openstack-network/admin/content/" rel="nofollow">http://docs.openstack.org/folsom/openstack-network/admin/content/</a>
      </div>
    </li>
    
    <li>
      <div>
        Object Storage管理员手册：<a title="http://docs.openstack.org/folsom/openstack-object-storage/admin/content/" href="http://docs.openstack.org/folsom/openstack-object-storage/admin/content/" rel="nofollow">http://docs.openstack.org/folsom/openstack-object-storage/admin/content/</a>
      </div>
    </li>
    
    <li>
      <div>
        OpenStack文档：<a title="http://docs.openstack.org/" href="http://docs.openstack.org/" rel="nofollow">http://docs.openstack.org/</a>
      </div>
    </li>
    
    <li>
      <div>
        OpenStack词汇表：<a title="http://docs.openstack.org/glossary/content/glossary.html" href="http://docs.openstack.org/glossary/content/glossary.html" rel="nofollow">http://docs.openstack.org/glossary/content/glossary.html</a>
      </div>
    </li>
    
    <li>
      <div>
        使用命令行管理openstack: <a title="http://docs.openstack.org/cli/quick-start/content/index.html" href="http://docs.openstack.org/cli/quick-start/content/index.html" rel="nofollow">http://docs.openstack.org/cli/quick-start/content/index.html</a>
      </div>
    </li>
    
    <li>
      <div>
        OpenStack Wiki: <a title="https://wiki.openstack.org/wiki/Main_Page" href="https://wiki.openstack.org/wiki/Main_Page" rel="nofollow">https://wiki.openstack.org/wiki/Main_Page</a>
      </div>
    </li>
  </ul>
</div>

## 简单安装 OpenStack {#简单安装_openstack}

### 环境设置 {#环境设置}

<div>
  <p>
    为了快速安装OpenStack,你要设置最快的apt源(或者设置yum源)和pypi源。
  </p>
  
  <ul>
    <li>
      <div>
        设置apt源：<a title="http://blog.ubuntusoft.com/ubuntu-update-source.html" href="http://blog.ubuntusoft.com/ubuntu-update-source.html" rel="nofollow">http://blog.ubuntusoft.com/ubuntu-update-source.html</a>
      </div>
    </li>
    
    <li>
      <div>
        设置pypi源：<a title="http://www.v2ex.com/t/75316" href="http://www.v2ex.com/t/75316" rel="nofollow">http://www.v2ex.com/t/75316</a>
      </div>
    </li>
  </ul>
  
  <p>
    你也可以搭建自己的apt源和pypi源：
  </p>
  
  <ul>
    <li>
      <div>
        搭建apt源：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://blog.ef.net/2012/10/26/unbutu-release-upgrade-with-local-apt-mirror.html" href="http://blog.ef.net/2012/10/26/unbutu-release-upgrade-with-local-apt-mirror.html" rel="nofollow">http://blog.ef.net/2012/10/26/unbutu-release-upgrade-with-local-apt-mirror.html</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://www.cnblogs.com/kulin/archive/2012/08/08/2628400.html" href="http://www.cnblogs.com/kulin/archive/2012/08/08/2628400.html" rel="nofollow">http://www.cnblogs.com/kulin/archive/2012/08/08/2628400.html</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        搭建pypi源：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="https://pypi.python.org/pypi/bandersnatch" href="https://pypi.python.org/pypi/bandersnatch" rel="nofollow">https://pypi.python.org/pypi/bandersnatch</a>
          </div>
        </li>
      </ul>
    </li>
  </ul>
</div>

### devstack 安装 {#devstack_安装}

<div>
  <ul>
    <li>
      <div>
        使用devstack安装 <a title="http://devstack.org" href="http://devstack.org/" rel="nofollow">http://devstack.org</a>
      </div>
    </li>
    
    <li>
      <div>
        阅读devstack.sh脚本 <a title="http://devstack.org" href="http://devstack.org/" rel="nofollow">http://devstack.org</a>
      </div>
    </li>
    
    <li>
      <div>
        screen的使用：<a title="http://www.9usb.net/201002/linux-screen-mingling.html" href="http://www.9usb.net/201002/linux-screen-mingling.html" rel="nofollow">http://www.9usb.net/201002/linux-screen-mingling.html</a>
      </div>
    </li>
  </ul>
  
  <p>
    devstack使用screen管理OpenStack各个服务，所以你要用screen调试OpenStack。
  </p>
</div>

### packstack(RHEL,CentOS) 安装 {#packstack_rhel_centos_安装}

<div>
  <ul>
    <li>
      <div>
        git仓库: <a title="https://github.com/stackforge/packstack" href="https://github.com/stackforge/packstack" rel="nofollow">https://github.com/stackforge/packstack</a>
      </div>
    </li>
    
    <li>
      <div>
        quickstart: <a title="http://openstack.redhat.com/Quickstart" href="http://openstack.redhat.com/Quickstart" rel="nofollow">http://openstack.redhat.com/Quickstart</a>
      </div>
    </li>
  </ul>
</div>

### deb包安装 {#deb包安装}

<div>
  <ul>
    <li>
      <div>
        <a title="http://wiki.stacklab.org/doku.php?id=stacklab:documentation:use-virtualbox-install-openstack" href="http://wiki.stacklab.org/doku.php?id=stacklab:documentation:use-virtualbox-install-openstack" rel="nofollow">使用VirtualBox安装OpenStack</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://wiki.stacklab.org/doku.php?id=stacklab:documentation:install-openstack-folsom-with-nova-network" href="http://wiki.stacklab.org/doku.php?id=stacklab:documentation:install-openstack-folsom-with-nova-network" rel="nofollow">在Ubuntu 12.04上安装OpenStack Folsom版(FlatDHCP+Multihost)</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://www.chenshake.com/ubuntu12-04-2-installed-openstack-grizzly-bridge-mode/" href="http://www.chenshake.com/ubuntu12-04-2-installed-openstack-grizzly-bridge-mode/" rel="nofollow">Ubuntu12.04.2 OpenStack Grizzly 安装（Bridge）</a>
      </div>
    </li>
  </ul>
</div>

### 源码安装 {#源码安装}

<div>
  <ul>
    <li>
      <div>
        官方教程: <a title="http://docs.openstack.org/install/" href="http://docs.openstack.org/install/" rel="nofollow">http://docs.openstack.org/install/</a>
      </div>
    </li>
  </ul>
</div>

## 调戏 OpenStack {#调戏_openstack}

<div>
  <ul>
    <li>
      <div>
        pdb：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://docs.python.org/2/library/pdb.html" href="http://docs.python.org/2/library/pdb.html" rel="nofollow">http://docs.python.org/2/library/pdb.html</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://blog.csdn.net/hackerain/article/details/8373597" href="http://blog.csdn.net/hackerain/article/details/8373597" rel="nofollow">http://blog.csdn.net/hackerain/article/details/8373597</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://www.ibm.com/developerworks/cn/linux/l-cn-pythondebugger/" href="http://www.ibm.com/developerworks/cn/linux/l-cn-pythondebugger/" rel="nofollow">http://www.ibm.com/developerworks/cn/linux/l-cn-pythondebugger/</a>
          </div>
        </li>
      </ul>
    </li>
  </ul>
</div>

## Python基本库 {#python基本库}

### WSGI {#wsgi}

<div>
  <ul>
    <li>
      <div>
        eventlet.wsgi: <a title="http://eventlet.net/doc/examples.html#wsgi-server" href="http://eventlet.net/doc/examples.html#wsgi-server" rel="nofollow">http://eventlet.net/doc/examples.html#wsgi-server</a>
      </div>
    </li>
    
    <li>
      <div>
        webob: <a title="http://webob.org/" href="http://webob.org/" rel="nofollow">http://webob.org/</a>
      </div>
    </li>
    
    <li>
      <div>
        pecan: <a title="http://pecanpy.org/" href="http://pecanpy.org/" rel="nofollow">http://pecanpy.org/</a>
      </div>
    </li>
    
    <li>
      <div>
        wsme: <a title="http://pythonhosted.org/WSME/" href="http://pythonhosted.org/WSME/" rel="nofollow">http://pythonhosted.org/WSME/</a>
      </div>
    </li>
    
    <li>
      <div>
        paste: <a title="http://pythonpaste.org/" href="http://pythonpaste.org/" rel="nofollow">http://pythonpaste.org/</a>
      </div>
    </li>
    
    <li>
      <div>
        routes: <a title="http://routes.readthedocs.org/en/latest/" href="http://routes.readthedocs.org/en/latest/" rel="nofollow">http://routes.readthedocs.org/en/latest/</a>
      </div>
    </li>
  </ul>
</div>

### 重要的库 {#重要的库}

<div>
  <ul>
    <li>
      <div>
        SQLAlchemy:<a title="http://www.sqlalchemy.org/" href="http://www.sqlalchemy.org/" rel="nofollow">http://www.sqlalchemy.org/</a>
      </div>
    </li>
    
    <li>
      <div>
        libvirt: <a title="http://libvirt.org/index.html" href="http://libvirt.org/index.html" rel="nofollow">http://libvirt.org/index.html</a>
      </div>
    </li>
    
    <li>
      <div>
        logging: <a title="http://docs.python.org/2/howto/logging-cookbook.html" href="http://docs.python.org/2/howto/logging-cookbook.html" rel="nofollow">http://docs.python.org/2/howto/logging-cookbook.html</a>
      </div>
    </li>
    
    <li>
      <div>
        greenlet: <a title="http://greenlet.readthedocs.org/en/latest/" href="http://greenlet.readthedocs.org/en/latest/" rel="nofollow">http://greenlet.readthedocs.org/en/latest/</a>
      </div>
    </li>
    
    <li>
      <div>
        eventlet: <a title="http://eventlet.net/" href="http://eventlet.net/" rel="nofollow">http://eventlet.net/</a>
      </div>
    </li>
    
    <li>
      <div>
        kombu: <a title="http://kombu.readthedocs.org/en/latest/" href="http://kombu.readthedocs.org/en/latest/" rel="nofollow">http://kombu.readthedocs.org/en/latest/</a>
      </div>
    </li>
    
    <li>
      <div>
        oslo.config: <a title="https://wiki.openstack.org/wiki/Oslo#oslo.config" href="https://wiki.openstack.org/wiki/Oslo#oslo.config" rel="nofollow">https://wiki.openstack.org/wiki/Oslo#oslo.config</a>
      </div>
    </li>
    
    <li>
      <div>
        stevedore: <a title="http://stevedore.readthedocs.org/en/latest/" href="http://stevedore.readthedocs.org/en/latest/" rel="nofollow">http://stevedore.readthedocs.org/en/latest/</a>
      </div>
    </li>
  </ul>
</div>

### TESTING {#testing}

<div>
  <ul>
    <li>
      <div>
        PythonTestingToolsTaxonomy: <a title="http://wiki.python.org/moin/PythonTestingToolsTaxonomy" href="http://wiki.python.org/moin/PythonTestingToolsTaxonomy" rel="nofollow">http://wiki.python.org/moin/PythonTestingToolsTaxonomy</a> (all in one)
      </div>
    </li>
    
    <li>
      <div>
        testtools：<a title="https://readthedocs.org/projects/testtools/" href="https://readthedocs.org/projects/testtools/" rel="nofollow">https://readthedocs.org/projects/testtools/</a>
      </div>
    </li>
    
    <li>
      <div>
        mox：<a title="http://code.google.com/p/pymox/wiki/MoxDocumentation" href="http://code.google.com/p/pymox/wiki/MoxDocumentation" rel="nofollow">http://code.google.com/p/pymox/wiki/MoxDocumentation</a>
      </div>
    </li>
    
    <li>
      <div>
        mock：<a title="http://www.voidspace.org.uk/python/mock/" href="http://www.voidspace.org.uk/python/mock/" rel="nofollow">http://www.voidspace.org.uk/python/mock/</a>
      </div>
    </li>
    
    <li>
      <div>
        tox：<a title="http://tox.readthedocs.org/en/latest/" href="http://tox.readthedocs.org/en/latest/" rel="nofollow">http://tox.readthedocs.org/en/latest/</a>
      </div>
    </li>
    
    <li>
      <div>
        fixtures：<a title="https://pypi.python.org/pypi/fixtures" href="https://pypi.python.org/pypi/fixtures" rel="nofollow">https://pypi.python.org/pypi/fixtures</a>
      </div>
    </li>
    
    <li>
      <div>
        testscenarios：<a title="https://pypi.python.org/pypi/testscenarios/" href="https://pypi.python.org/pypi/testscenarios/" rel="nofollow">https://pypi.python.org/pypi/testscenarios/</a>
      </div>
    </li>
    
    <li>
      <div>
        nose：<a title="https://nose.readthedocs.org/en/latest/" href="https://nose.readthedocs.org/en/latest/" rel="nofollow">https://nose.readthedocs.org/en/latest/</a>
      </div>
    </li>
    
    <li>
      <div>
        testrepository：<a title="https://testrepository.readthedocs.org/en/latest/MANUAL.html" href="https://testrepository.readthedocs.org/en/latest/MANUAL.html" rel="nofollow">https://testrepository.readthedocs.org/en/latest/MANUAL.html</a>
      </div>
    </li>
  </ul>
</div>

## OpenStack基础组件 {#openstack基础组件}

<div>
  <p>
    在OpenStack中，有一个重要的项目叫做Oslo(原名是openstack-common),给OpenStack其他项目提供基础组件。
  </p>
  
  <ul>
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Oslo" href="https://wiki.openstack.org/wiki/Oslo" rel="nofollow">https://wiki.openstack.org/wiki/Oslo</a>
      </div>
    </li>
  </ul>
</div>

### RPC组件 {#rpc组件}

<div>
  <ul>
    <li>
      <div>
        <a title="http://wiki.ustack.com/doku.php?id=rpc%E6%A8%A1%E5%9D%97" href="http://wiki.ustack.com/doku.php?id=rpc%E6%A8%A1%E5%9D%97" rel="nofollow">RPC组件</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://blog.ftofficer.com/2010/03/translation-rabbitmq-python-rabbits-and-warrens/" href="http://blog.ftofficer.com/2010/03/translation-rabbitmq-python-rabbits-and-warrens/" rel="nofollow">http://blog.ftofficer.com/2010/03/translation-rabbitmq-python-rabbits-and-warrens/</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://www.rabbitmq.com/tutorials/tutorial-six-python.html" href="http://www.rabbitmq.com/tutorials/tutorial-six-python.html" rel="nofollow">http://www.rabbitmq.com/tutorials/tutorial-six-python.html</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://docs.openstack.org/developer/nova/devref/rpc.html" href="http://docs.openstack.org/developer/nova/devref/rpc.html" rel="nofollow">http://docs.openstack.org/developer/nova/devref/rpc.html</a>
      </div>
    </li>
  </ul>
</div>

### WSGI {#wsgi1}

<div>
  <ul>
    <li>
      <div>
        <a title="http://archimedeanco.com/wsgi-tutorial/" href="http://archimedeanco.com/wsgi-tutorial/" rel="nofollow">http://archimedeanco.com/wsgi-tutorial/</a>
      </div>
    </li>
  </ul>
</div>

## OpenStack 代码规范 {#openstack_代码规范}

<div>
  <ul>
    <li>
      <div>
        Python PEP8 规范: <a title="http://www.python.org/dev/peps/pep-0008/" href="http://www.python.org/dev/peps/pep-0008/" rel="nofollow">http://www.python.org/dev/peps/pep-0008/</a>
      </div>
    </li>
  </ul>
  
  <ul>
    <li>
      <div>
        OpenStack HACKING 规范: <a title="https://github.com/openstack-dev/hacking/blob/master/HACKING.rst" href="https://github.com/openstack-dev/hacking/blob/master/HACKING.rst" rel="nofollow">https://github.com/openstack-dev/hacking/blob/master/HACKING.rst</a>
      </div>
    </li>
  </ul>
</div>

## Python 深入学习 {#python_深入学习}

<div>
  <p>
    理解python中optparse.OptionParser类。<br /> <a title="http://docs.python.org/library/optparse.html" href="http://docs.python.org/library/optparse.html" rel="nofollow">http://docs.python.org/library/optparse.html</a>
  </p>
  
  <p>
    理解collections.Mapping类。<br /> <a title="http://docs.python.org/library/collections.html" href="http://docs.python.org/library/collections.html" rel="nofollow">http://docs.python.org/library/collections.html</a>
  </p>
  
  <p>
    分析浅拷贝，深拷贝<br /> <a title="http://blog.csdn.net/winterttr/article/details/2590741" href="http://blog.csdn.net/winterttr/article/details/2590741" rel="nofollow">http://blog.csdn.net/winterttr/article/details/2590741</a><br /> <a title="http://longmans1985.blog.163.com/blog/static/70605475200991603624942/" href="http://longmans1985.blog.163.com/blog/static/70605475200991603624942/" rel="nofollow">http://longmans1985.blog.163.com/blog/static/70605475200991603624942/</a><br /> <a title="http://book.51cto.com/art/200806/77233.htm" href="http://book.51cto.com/art/200806/77233.htm" rel="nofollow">http://book.51cto.com/art/200806/77233.htm</a>
  </p>
  
  <p>
    LoggerAdapter类<br /> <a title="http://docs.python.org/howto/logging-cookbook.html#context-info" href="http://docs.python.org/howto/logging-cookbook.html#context-info" rel="nofollow">http://docs.python.org/howto/logging-cookbook.html#context-info</a>中。
  </p>
  
  <p>
    介绍rabbitmq<br /> <a title="http://blog.ftofficer.com/2010/03/translation-rabbitmq-python-rabbits-and-warrens/" href="http://blog.ftofficer.com/2010/03/translation-rabbitmq-python-rabbits-and-warrens/" rel="nofollow">http://blog.ftofficer.com/2010/03/translation-rabbitmq-python-rabbits-and-warrens/</a><br /> <a title="http://kombu.readthedocs.org/en/latest/introduction.html#synopsis" href="http://kombu.readthedocs.org/en/latest/introduction.html#synopsis" rel="nofollow">http://kombu.readthedocs.org/en/latest/introduction.html#synopsis</a>
  </p>
  
  <p>
    Python Decorators入门<br /> <a title="http://blog.csdn.net/beckel/article/details/3585352" href="http://blog.csdn.net/beckel/article/details/3585352" rel="nofollow">http://blog.csdn.net/beckel/article/details/3585352</a>
  </p>
  
  <p>
    Python @classmethod @staticmethod的区别。
  </p>
  
  <p>
    五分钟理解元类（Metaclasses）<br /> <a title="http://www.cnblogs.com/coderzh/archive/2008/12/07/1349735.html" href="http://www.cnblogs.com/coderzh/archive/2008/12/07/1349735.html" rel="nofollow">http://www.cnblogs.com/coderzh/archive/2008/12/07/1349735.html</a>
  </p>
  
  <p>
    nova中用到的python知识<br /> <a title="http://canx.me/2011/12/%E4%B8%80%E4%BA%9Bpython/" href="http://canx.me/2011/12/%E4%B8%80%E4%BA%9Bpython/" rel="nofollow">http://canx.me/2011/12/%E4%B8%80%E4%BA%9Bpython/</a>
  </p>
  
  <p>
    python中类的总结<br /> <a title="http://ipseek.blog.51cto.com/1041109/802243" href="http://ipseek.blog.51cto.com/1041109/802243" rel="nofollow">http://ipseek.blog.51cto.com/1041109/802243</a>
  </p>
  
  <p>
    with的总结<br /> <a title="http://effbot.org/zone/python-with-statement.htm" href="http://effbot.org/zone/python-with-statement.htm" rel="nofollow">http://effbot.org/zone/python-with-statement.htm</a>
  </p>
  
  <p>
    Pool类<br /> <a title="http://nullege.com/codes/search/eventlet.pools.Pool" href="http://nullege.com/codes/search/eventlet.pools.Pool" rel="nofollow">http://nullege.com/codes/search/eventlet.pools.Pool</a>
  </p>
  
  <p>
    paste模块<br /> <a title="http://pythonpaste.org/" href="http://pythonpaste.org/" rel="nofollow">http://pythonpaste.org/</a>
  </p>
  
  <p>
    python魔术方法<br /> <a title="http://pycoders-weekly-chinese.readthedocs.org/en/latest/issue6/a-guide-to-pythons-magic-methods.html" href="http://pycoders-weekly-chinese.readthedocs.org/en/latest/issue6/a-guide-to-pythons-magic-methods.html" rel="nofollow">http://pycoders-weekly-chinese.readthedocs.org/en/latest/issue6/a-guide-to-pythons-magic-methods.html</a>
  </p>
  
  <p>
    Routes模块<br /> <a title="http://routes.readthedocs.org/en/latest/index.html" href="http://routes.readthedocs.org/en/latest/index.html" rel="nofollow">http://routes.readthedocs.org/en/latest/index.html</a>
  </p>
  
  <p>
    yield学习
  </p>
  
  <ul>
    <li>
      <div>
        <a title="http://www.pythonclub.org/python-basic/yield" href="http://www.pythonclub.org/python-basic/yield" rel="nofollow">http://www.pythonclub.org/python-basic/yield</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://blog.donews.com/limodou/archive/2006/09/04/1028747.aspx" href="http://blog.donews.com/limodou/archive/2006/09/04/1028747.aspx" rel="nofollow">http://blog.donews.com/limodou/archive/2006/09/04/1028747.aspx</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://www.ibm.com/developerworks/cn/opensource/os-cn-python-yield/" href="http://www.ibm.com/developerworks/cn/opensource/os-cn-python-yield/" rel="nofollow">http://www.ibm.com/developerworks/cn/opensource/os-cn-python-yield/</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://www.jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/" href="http://www.jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/" rel="nofollow">http://www.jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/</a>
      </div>
    </li>
  </ul>
</div>

# 4 OpenStack 整体架构 {#openstack_整体架构}

## 架构图 {#架构图}

<div>
  <p>
    必看：
  </p>
  
  <ul>
    <li>
      <div>
        <a title="http://ken.pepple.info/openstack/2012/09/25/openstack-folsom-architecture/" href="http://ken.pepple.info/openstack/2012/09/25/openstack-folsom-architecture/" rel="nofollow">http://ken.pepple.info/openstack/2012/09/25/openstack-folsom-architecture/</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://www.solinea.com/2013/06/15/openstack-grizzly-architecture-revisited/" href="http://www.solinea.com/2013/06/15/openstack-grizzly-architecture-revisited/" rel="nofollow">http://www.solinea.com/2013/06/15/openstack-grizzly-architecture-revisited/</a>
      </div>
    </li>
  </ul>
  
  <p>
    OpenStack架构图，你可以点击放大。
  </p>
  
  <p>
    <a href="http://www.ustack.com/wp-content/uploads/2013/08/openstack-logical-arch-folsom.jpg"><img alt="openstack-logical-arch-folsom" src="http://www.ustack.com/wp-content/uploads/2013/08/openstack-logical-arch-folsom-1024x626.jpg" width="625" height="382" /></a>
  </p>
</div>

## 工作流 {#工作流}

### Keystone Workflow {#keystone_workflow}

<div>
  <p>
    必看：
  </p>
  
  <ul>
    <li>
      <div>
        <a title="https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_keystone_workflow_token_scoping?lang=zh" href="https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_keystone_workflow_token_scoping?lang=zh" rel="nofollow">https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_keystone_workflow_token_scoping?lang=zh</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://docs.openstack.org/trunk/openstack-compute/admin/content/keystone-concepts.html" href="http://docs.openstack.org/trunk/openstack-compute/admin/content/keystone-concepts.html" rel="nofollow">http://docs.openstack.org/trunk/openstack-compute/admin/content/keystone-concepts.html</a>
      </div>
    </li>
  </ul>
  
  <p>
    点击可看大图。
  </p>
  
  <p>
    <a href="http://www.ustack.com/wp-content/uploads/2013/08/SCH_5002_V00_NUAC-Keystone.png"><img alt="SCH_5002_V00_NUAC-Keystone" src="http://www.ustack.com/wp-content/uploads/2013/08/SCH_5002_V00_NUAC-Keystone-1024x693.png" width="625" height="422" /></a>
  </p>
</div>

### Nova Workflow {#nova_workflow}

<div>
  <p>
    必看：
  </p>
  
  <ul>
    <li>
      <div>
        <a title="https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_nova_api?lang=en" href="https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_nova_api?lang=en" rel="nofollow">https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_nova_api?lang=en</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="http://ilearnstack.com/2013/04/26/request-flow-for-provisioning-instance-in-openstack/comment-page-1/" href="http://ilearnstack.com/2013/04/26/request-flow-for-provisioning-instance-in-openstack/comment-page-1/" rel="nofollow">http://ilearnstack.com/2013/04/26/request-flow-for-provisioning-instance-in-openstack/comment-page-1/</a>
      </div>
    </li>
  </ul>
  
  <p>
    nova-api处理 REST 请求。
  </p>
  
  <p>
    <a href="http://www.ustack.com/wp-content/uploads/2013/08/nova-server-request.jpeg"><img alt="nova-server-request" src="http://www.ustack.com/wp-content/uploads/2013/08/nova-server-request.jpeg" width="919" height="534" /></a>
  </p>
  
  <p>
    nova创建虚拟机的工作流。
  </p>
  
  <p>
    <a href="http://www.ustack.com/wp-content/uploads/2013/08/request-flow1.png"><img alt="request-flow1" src="http://www.ustack.com/wp-content/uploads/2013/08/request-flow1-1024x665.png" width="625" height="405" /></a>
  </p>
</div>

## OpenStack 核心项目 {#openstack_核心项目}

<div>
  <p>
    对各个项目简要分析：<a title="http://www.slideshare.net/randybias/state-of-the-stack-april-2013" href="http://www.slideshare.net/randybias/state-of-the-stack-april-2013" rel="nofollow">http://www.slideshare.net/randybias/state-of-the-stack-april-2013</a>
  </p>
  
  <p>
    核心项目的分析：
  </p>
  
  <ul>
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Keystone" href="https://wiki.openstack.org/wiki/Keystone" rel="nofollow">Keystone</a>：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://docs.openstack.org/developer/keystone/" href="http://docs.openstack.org/developer/keystone/" rel="nofollow">http://docs.openstack.org/developer/keystone/</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://www.slideshare.net/openstackindia/openstack-keystone-identity-service" href="http://www.slideshare.net/openstackindia/openstack-keystone-identity-service" rel="nofollow">http://www.slideshare.net/openstackindia/openstack-keystone-identity-service</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Glance" href="https://wiki.openstack.org/wiki/Glance" rel="nofollow">Glance</a>：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://docs.openstack.org/developer/glance/" href="http://docs.openstack.org/developer/glance/" rel="nofollow">http://docs.openstack.org/developer/glance/</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Nova" href="https://wiki.openstack.org/wiki/Nova" rel="nofollow">Nova</a>：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://docs.openstack.org/developer/nova/" href="http://docs.openstack.org/developer/nova/" rel="nofollow">http://docs.openstack.org/developer/nova/</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_nova_scheduler_and_its_algorithm27?lang=en" href="https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_nova_scheduler_and_its_algorithm27?lang=en" rel="nofollow">https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_nova_scheduler_and_its_algorithm27?lang=en</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Cinder" href="https://wiki.openstack.org/wiki/Cinder" rel="nofollow">Cinder</a>：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://docs.openstack.org/developer/cinder/" href="http://docs.openstack.org/developer/cinder/" rel="nofollow">http://docs.openstack.org/developer/cinder/</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="https://wiki.openstack.org/w/images/3/3b/Cinder-grizzly-deep-dive-pub.pdf" href="https://wiki.openstack.org/w/images/3/3b/Cinder-grizzly-deep-dive-pub.pdf" rel="nofollow">Cinder grizzly deep dive pub</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Neutron" href="https://wiki.openstack.org/wiki/Neutron" rel="nofollow">Neutron</a>：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://docs.openstack.org/developer/neutron/" href="http://docs.openstack.org/developer/neutron/" rel="nofollow">http://docs.openstack.org/developer/neutron/</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://www.slideshare.net/openstackindia/openstack-quantum-16710792" href="http://www.slideshare.net/openstackindia/openstack-quantum-16710792" rel="nofollow">http://www.slideshare.net/openstackindia/openstack-quantum-16710792</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://www.slideshare.net/lewtucker/openstack-quantum-network-service" href="http://www.slideshare.net/lewtucker/openstack-quantum-network-service" rel="nofollow">http://www.slideshare.net/lewtucker/openstack-quantum-network-service</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://www.slideshare.net/openstackindia/openstack-quantum-18418306" href="http://www.slideshare.net/openstackindia/openstack-quantum-18418306" rel="nofollow">http://www.slideshare.net/openstackindia/openstack-quantum-18418306</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Horizon" href="https://wiki.openstack.org/wiki/Horizon" rel="nofollow">Horizon</a>：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://docs.openstack.org/developer/horizon/" href="http://docs.openstack.org/developer/horizon/" rel="nofollow">http://docs.openstack.org/developer/horizon/</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Swift" href="https://wiki.openstack.org/wiki/Swift" rel="nofollow">Swift</a>：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://docs.openstack.org/developer/swift/" href="http://docs.openstack.org/developer/swift/" rel="nofollow">http://docs.openstack.org/developer/swift/</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://blog.csdn.net/alex890714/article/details/7314780" href="http://blog.csdn.net/alex890714/article/details/7314780" rel="nofollow">http://blog.csdn.net/alex890714/article/details/7314780</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://events.csdn.net/OpenStack/%E6%9D%A8%E9%9B%A8-Swift%E6%9E%B6%E6%9E%84%E4%B8%8E%E5%AE%9E%E8%B7%B5.pdf" href="http://events.csdn.net/OpenStack/%E6%9D%A8%E9%9B%A8-Swift%E6%9E%B6%E6%9E%84%E4%B8%8E%E5%AE%9E%E8%B7%B5.pdf" rel="nofollow">Swift架构与实践</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Oslo" href="https://wiki.openstack.org/wiki/Oslo" rel="nofollow">Oslo</a>：
      </div>
    </li>
  </ul>
  
  <p>
    通用机制的分析：
  </p>
  
  <ul>
    <li>
      <div>
        quota: <a title="http://blog.csdn.net/hackerain/article/details/8223125" href="http://blog.csdn.net/hackerain/article/details/8223125" rel="nofollow">http://blog.csdn.net/hackerain/article/details/8223125</a>
      </div>
    </li>
    
    <li>
      <div>
        policy: <a title="http://blog.csdn.net/hackerain/article/details/8241691" href="http://blog.csdn.net/hackerain/article/details/8241691" rel="nofollow">http://blog.csdn.net/hackerain/article/details/8241691</a>
      </div>
    </li>
  </ul>
</div>

# 5 OpenStack 部署/管理 {#openstack_部署_管理}

## OpenStack 自动化部署 {#openstack_自动化部署}

<div>
  <p>
    Puppet:
  </p>
  
  <ul>
    <li>
      <div>
        <a title="https://wiki.openstack.org/wiki/Puppet-openstack" href="https://wiki.openstack.org/wiki/Puppet-openstack" rel="nofollow">https://wiki.openstack.org/wiki/Puppet-openstack</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="https://github.com/stackforge/puppet-openstack" href="https://github.com/stackforge/puppet-openstack" rel="nofollow">https://github.com/stackforge/puppet-openstack</a>
      </div>
    </li>
    
    <li>
      <div>
        <a title="https://puppetlabs.com/solutions/openstack/" href="https://puppetlabs.com/solutions/openstack/" rel="nofollow">https://puppetlabs.com/solutions/openstack/</a>
      </div>
    </li>
  </ul>
  
  <p>
    Fule: Mirantis出品的部署工具，从裸机到OpenStack组件再到HA全部搞定
  </p>
  
  <ul>
    <li>
      <div>
        <a title="https://fuel.mirantis.com/" href="https://fuel.mirantis.com/" rel="nofollow">https://fuel.mirantis.com/</a>
      </div>
    </li>
  </ul>
</div>

## OpenStack 监控 {#openstack_监控}

<div>
  <ul>
    <li>
      <div>
        OpenStack 监控: <a title="http://www.mirantis.com/blog/openstack-monitoring/" href="http://www.mirantis.com/blog/openstack-monitoring/" rel="nofollow">http://www.mirantis.com/blog/openstack-monitoring/</a>
      </div>
    </li>
  </ul>
</div>

# 6 参与 OpenStack 社区 {#参与_openstack_社区}

<div>
  <p>
    都在这里:<a title="https://wiki.openstack.org/wiki/Main_Page" href="https://wiki.openstack.org/wiki/Main_Page" rel="nofollow">https://wiki.openstack.org/wiki/Main_Page</a>
  </p>
  
  <ul>
    <li>
      <div>
        山头： <a title="https://review.openstack.org/#/admin/groups" href="https://review.openstack.org/#/admin/groups" rel="nofollow">https://review.openstack.org/#/admin/groups</a>
      </div>
    </li>
    
    <li>
      <div>
        向社区提交Patch：<a title="https://wiki.openstack.org/wiki/How_To_Contribute" href="https://wiki.openstack.org/wiki/How_To_Contribute" rel="nofollow">https://wiki.openstack.org/wiki/How_To_Contribute</a>
      </div>
    </li>
    
    <li>
      <div>
        gerrit的使用：<a title="https://wiki.openstack.org/wiki/Gerrit_Workflow" href="https://wiki.openstack.org/wiki/Gerrit_Workflow" rel="nofollow">https://wiki.openstack.org/wiki/Gerrit_Workflow</a>
      </div>
    </li>
    
    <li>
      <div>
        Review别人的Patch：<a title="https://review.openstack.org" href="https://review.openstack.org/" rel="nofollow">https://review.openstack.org</a>
      </div>
    </li>
    
    <li>
      <div>
        参与IRC Meeting：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="https://wiki.openstack.org/wiki/Meetings" href="https://wiki.openstack.org/wiki/Meetings" rel="nofollow">https://wiki.openstack.org/wiki/Meetings</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="https://wiki.openstack.org/wiki/Mailing_Lists" href="https://wiki.openstack.org/wiki/Mailing_Lists" rel="nofollow">https://wiki.openstack.org/wiki/Mailing_Lists</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="https://wiki.openstack.org/wiki/People" href="https://wiki.openstack.org/wiki/People" rel="nofollow">https://wiki.openstack.org/wiki/People</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        参与邮件列表讨论：<a title="https://wiki.openstack.org/wiki/Mailing_Lists" href="https://wiki.openstack.org/wiki/Mailing_Lists" rel="nofollow">https://wiki.openstack.org/wiki/Mailing_Lists</a>
      </div>
    </li>
    
    <li>
      <div>
        跟踪OpenStack项目的发展：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="http://www.openstack.org/blog/" href="http://www.openstack.org/blog/" rel="nofollow">http://www.openstack.org/blog/</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://planet.openstack.org/" href="http://planet.openstack.org/" rel="nofollow">http://planet.openstack.org/</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="https://wiki.openstack.org/wiki/Special:RecentChanges" href="https://wiki.openstack.org/wiki/Special:RecentChanges" rel="nofollow">https://wiki.openstack.org/wiki/Special:RecentChanges</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://github.com/openstack" href="http://github.com/openstack" rel="nofollow">http://github.com/openstack</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="https://github.com/stackforge/" href="https://github.com/stackforge/" rel="nofollow">https://github.com/stackforge/</a> (You will like it)
          </div>
        </li>
        
        <li>
          <div>
            <a title="https://github.com/openstack-dev/" href="https://github.com/openstack-dev/" rel="nofollow">https://github.com/openstack-dev/</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="https://github.com/openstack-infra" href="https://github.com/openstack-infra" rel="nofollow">https://github.com/openstack-infra</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        学习CI：<a title="http://ci.openstack.org/" href="http://ci.openstack.org/" rel="nofollow">http://ci.openstack.org/</a>
      </div>
    </li>
  </ul>
</div>

# 7 OpenStack 二次开发 {#openstack_二次开发}

<div>
  <ul>
    <li>
      <div>
        开发Nova的扩展API：
      </div>
      
      <ul>
        <li>
          <div>
            <a title="https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_nova_api?lang=zh" href="https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_nova_api?lang=zh" rel="nofollow">https://www.ibm.com/developerworks/community/blogs/e93514d3-c4f0-4aa0-8844-497f370090f5/entry/openstack_nova_api?lang=zh</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="https://wiki.openstack.org/wiki/WritingRequestExtensions" href="https://wiki.openstack.org/wiki/WritingRequestExtensions" rel="nofollow">https://wiki.openstack.org/wiki/WritingRequestExtensions</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://stephanfr.com/2013/04/07/creating-an-openstack-keystone-helloworld-extension/" href="http://stephanfr.com/2013/04/07/creating-an-openstack-keystone-helloworld-extension/" rel="nofollow">http://stephanfr.com/2013/04/07/creating-an-openstack-keystone-helloworld-extension/</a>
          </div>
        </li>
        
        <li>
          <div>
            <a title="http://www.cnblogs.com/willier/archive/2013/05/22/3092961.html" href="http://www.cnblogs.com/willier/archive/2013/05/22/3092961.html" rel="nofollow">http://www.cnblogs.com/willier/archive/2013/05/22/3092961.html</a>
          </div>
        </li>
      </ul>
    </li>
    
    <li>
      <div>
        开发Cinder的driver：
      </div>
      
      <ul>
        <li>
          <div>
            新的driver必须满足 <a title="https://github.com/openstack/cinder/blob/master/doc/source/devref/drivers.rst" href="https://github.com/openstack/cinder/blob/master/doc/source/devref/drivers.rst" rel="nofollow">Minimum Features</a>,参考同类型的driver，依葫芦画瓢。
          </div>
        </li>
      </ul>
    </li>
  </ul>
</div>

# 8 OpenStack 生态圈 {#openstack_生态圈}

<div>
  <ul>
    <li>
      <div>
        OpenStack幕后的公司：<a title="http://www.chenshake.com/behind-the-openstack-company" href="http://www.chenshake.com/behind-the-openstack-company" rel="nofollow">http://www.chenshake.com/behind-the-openstack-company</a>
      </div>
    </li>
    
    <li>
      <div>
        State of The Stack：<a title="http://www.slideshare.net/randybias/state-of-the-stack-april-2013" href="http://www.slideshare.net/randybias/state-of-the-stack-april-2013" rel="nofollow">http://www.slideshare.net/randybias/state-of-the-stack-april-2013</a> (一针见血)
      </div>
    </li>
    
    <li>
      <div>
        OpenStack贡献排行榜：<a title="http://stackalytics.com/" href="http://stackalytics.com/" rel="nofollow">http://stackalytics.com/</a>
      </div>
    </li>
    
    <li>
      <div>
        OpenStack实践分享：<a title="http://www.mirantis.com/blog/" href="http://www.mirantis.com/blog/" rel="nofollow">http://www.mirantis.com/blog/</a> (mirantis是目前最成功的OpenStack系统集成商)
      </div>
    </li>
  </ul>
</div>

参考：<http://www.ustack.com/openstack_hacker/>