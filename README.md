<a href="https://github.com/TryGhost/Ghost"><img src="https://cloud.githubusercontent.com/assets/120485/6622822/c4c639fe-c8e7-11e4-9e64-5bec06c8b4c3.png" alt="Ghost" /></a>
<a href="https://travis-ci.org/TryGhost/Ghost"><img align="right" src="https://travis-ci.org/TryGhost/Ghost.svg?branch=master" alt="Build status" /></a>

![Ghost Screenshot](https://cloud.githubusercontent.com/assets/120485/6626466/6dae46b2-c8ff-11e4-8c7c-8dd63b215f7b.jpg)

![Ghost is a simple, powerful publishing platform that allows you to share your stories with the world.](https://cloud.githubusercontent.com/assets/120485/6626501/b2bb072c-c8ff-11e4-8e1a-2e78e68fd5c3.png)

Ghost 目由非盈利性组织 **Ghost Foundation** 和一群优秀的独立[贡献者](https://github.com/TryGhost/Ghost/contributors)共同维护。我们正在尽最大努力让在线内容创作变得更好。

# 快速部署，完整安装包

安装前请确保已经安装了 Node.js - 我们建议使用 **Node v0.10.x** 的最新版本。

Ghost 同时也支持 **Node v0.12** 和 **io.js v1.2** ，但是请注意，这些版本很有可能导致安装失败。如果遇到问题，请到[论坛](https://ghost.org/forum/installation/)寻求帮助。

1. 在你的服务器端希望的位置 git clone https://github.com/sasuke6/ghost
1. 使用Upstart守护Ghost，极力推荐此种方式，使用foerver进程有时会使服务器CPU使用率过高，而且也不用担心服务器宕机造成Ghost停止
  
   >Upstart is an event-based replacement for the /sbin/init daemon which handles starting of tasks and services during boot, stopping them during shutdown and supervising them while the system is running.
   
首先进入`etc/init`，然后执行以下指令：
   
    nano ghost.conf

然后复制/粘贴以下配置信息：

	description "Ghost Blogging Platform"  
	author      "www.hsuchihyung.cn"  
	start on runlevel [2345]  
	stop on shutdown

	respawn  
	respawn limit 99 5

	script  
       cd /your/ghost/folder
       npm start --production 2>&1 >> /dev/null
	end script  

*  `description`描述信息
*  `npm start --production 2>&1 >> /dev/null`启动 Ghost，并将 stdout 和 stderr 中输出的信息全部丢弃。`/dev/null`就像一个黑洞，任何写入的内容都将消失。这里我们的用意是不记录任何日志。

保存上述文件。然后启动Ghost：
	
	sudo start ghost
	
你会看到类似下面的输出信息：
	
	ghost start/running, process 11290
	
`11290`是进程ID，每次运行可能会不同。但是，看到这条消息就说明Ghost正常启动了。

##其他指令
关闭Upstart服务的指令为：

	sudo stop ghost
	
重启Upstart服务的指令为：

	sudo restart ghost
	
最后，不用`npm install --production`和`npm start --production`,已经集成Ghost依赖包，可以直接启动使用，打开你的域名即可。


# 其他方式部署 Ghost

![Ghost(Pro) + DigitalOcean](https://cloud.githubusercontent.com/assets/120485/8180331/d6674e32-1414-11e5-8ce4-2250e9994906.png)

Ghost 官方支持的 **[Ghost(Pro)](https://ghost.org/pricing/)** 服务能够帮你节约大量时间，只需点几下鼠标就能部署一个 Ghost 实例到 [DigitalOcean](https://digitalocean.com) 的服务器上，并且还可以免费享受到全球化的 CDN 服务。

从 **Ghost(Pro)** 所获得的所有收益都将用于 Ghost 基金 -- 一个非营利性的组织，为 Ghost 的开发和维护提供支持。

如果你希望自己部署 Ghost，可以参考[这里](http://support.ghost.org/deploying-ghost/) 。


# 保持更新

当 Ghost 有新版本发布时，请参考 [升级指南](http://support.ghost.org/how-to-upgrade/) 以了解如何升级 Ghost。

你可以加入 [问答社区（中文）](http://wenda.ghostchina.com/) 和其他 Ghost 用户交流，或者在 [public Slack team](https://ghost.org/slack/) 与 Ghost 开发者沟通。我们每周二下午 5:30 都会在 Slack 上开碰头会。请注意，我们说的是`伦敦时间`。

每次有新版本都会在 [技术博客](http://dev.ghost.org/tag/releases/) 上公布。你可以通过邮件订阅或者在 Twitter 上关注 [@TryGhost_Dev](https://twitter.com/tryghost_dev)。

# 版权 & 协议

Copyright (c) 2013-2016 Ghost Foundation - Released under the [MIT license](LICENSE).

# 中文版本及插件

Copyright (c) 2013-2016 Ghost 中国/中文网 - 采用 `MIT 许可协议` 发布。

#感谢

感谢Ghostchina和其他开发者的无私分享。


