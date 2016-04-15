title: ipchecker
date: 2016-04-15 14:34:25
catagory: "tech"
tags: "index"
---

- 大概两年以前，我把奶奶家的台式机搬到自己家里，重新装上了 Ubuntu 系统，希望能够做一个类似服务器一样的东西，然后家里人可以在上面传点照片，文件什么的。后来发现家里的管带供应商给的 IP 一直在变。我不在家的时候变了，服务器就直接失联。当时我还没有用 AWS，整个人都是崩溃的。
- 最近有了新电脑，就考虑可以把旧电脑放在寝室刷六维，然后开各种共享来从外部访问。突然发现这是同一个问题的我马上想到了解决方案：通过一个 server-client 架构在固定 IP 的服务器上维护浮动的 IP，这样就可以方便的访问浮动 IP 的机器啦。由于有了固定 IP 的机器（AWS 上的 SS server），我们（终于）可以实现这个想法了噜。
- Server 方面用 `web.py` 来简单的搭一个接受 client 的 POST 更新 IP 信息并且可以通过不同路径的 GET 来查询的服务。因为数据量不大（懒），没有用数据库存储而是直接写到文件里了。不要在意细节。
- Client 用 requests 做一个定时向 server POST 自己的 IP 信息的程序然后扔到后台跑就好了。
- 现在 client 的信息包括两部分
	- 用十分 naive 的方法从 ifconfig 的结果中找到的可能能够访问的机器的 IP，关键字为 `ip`，通过 `/{machine_name}/ip` 来访问。
	- ifconfig 的全部输出，关键字为 `ifconfig`，通过 `/{machine_name}/if` 来访问。
- 接下来要做的大概有几点：
	- 安全性问题，比如换数据库啦，对 POST 信息加密啦之类的。
	- 增加新的组件，可以自动向 server 请求信息并更新自己的 hosts 文件。
- 具体的项目进度和代码详见 [ipchecker](http://github.com/kevinxuxuxu/ipchecker)

- 最近在听[平野绫](http://music.163.com/#/artist?id=16400)的歌，感觉团长声音真实赞。由于网易云音乐的插件出现了迷のbug，就贴两个链接吧：[God knows](http://music.163.com/#/song?id=27876224)，[Star way to heaven](http://music.163.com/#/song?id=27876221)