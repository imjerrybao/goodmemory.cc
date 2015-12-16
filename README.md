# WHAT

当学习完hugo后，我就打算做一个自动化的hugo流程。
这个repo是[http://www.goodmemory.cc](http://www.goodmemory.cc)的文章在线编辑器和仓库。在这里写的文章将会自动同步到目标网站，并转化成静态网页。

# HOW

1. 设置github的webservice hook。在收到push事件后，向目标网站发消息。
2. 目标网站收到消息后git pull，得到最新的文章内容
3. 调用本地的hugo，将markdown文章转化成html静态页面，并自动部署

至此，只要在这里更新的内容，就自动转化成网站页面了。

have fun！
