---
layout: post
title: 技术人如何使用jekyll搭建自己的博客
category: Linux
tags: [Linux]
excerpt: 技术人如何使用jekyll搭建自己的博客
---

# 一、博客搭建 #

我的搭建环境是：

win10电脑 博客的基本环境（编写博客的环境）

Linux服务器 博客基本环境（编译博客的环境）+nginx+自动化部署环境

# 二、win10博客环境的安装 #

## 1、建立Ruby环境 ##

下载Ruby的Windows安装包，注意32位还是64位。安装时记得Add Ruby executables to your PATH! 安装完成后打开命令行，执行

	ruby -v 

下载地址：

<http://rubyinstaller.org/downloads/>

## 2、安装Ruby DevKit ##

下载DEVELOPMENT KIT后，解压缩到任意目录，注意对应32位还是64位。打开命令行，转到DevKit解压后的目录，执行


	ruby dk.rb init

系统会在对应的目录中生成config.xml文件，用文本编辑器打开，修改自己的ruby安装路径，如下：


	#
	#Example:
	#
	#----
	#_C:/ruby19trunk
	#_C:/ruby192dev
	#
	---
	-C:/Ruby23-x64

修改完毕后，继续执行

	ruby dk.rb install	

## 3、配置RubyGems的镜像gems.ruby-china.org ##

如果遇到Windows下证书无法验证问题（certificate verify failed）,首先下载证书http://curl.haxx.se/ca/cacert.pem,然后在环境变量里设置SSL_CERT_FILE这个环境变量，并指向cacert.pem文件。

执行

	gem sources --add http://gems.ruby-china.com/ --remove http://rubygems.org/

检查gem的源，确保只有gems.ruby-china.com

	gem sources -l

更新完RubyGems之后，可以顺便做个升级

	update --system gem-v

## 4、安装Jekyll  ##

	gem install jekyll

## 5、安装Bundler ##

	gem install bundler

# 三、项目本地运行 #

## 1、修改Gemfile.lock文件 ##

将其中nokogiri的版本号，由1.6.7修改为1.6.8.1

将remote项中的地址修改为：https://gems.ruby-china.com/

Gemfile文件中source项中的地址可以修改为：https://gems.ruby-china.com/

## 2、添加bower_components文件夹 ##

可以去https://github.com/DONGChuan/DONGChuan.github.io项目下载，或者使用bower install来安装

## 3、运行 ##

打开命令行，进入项目对应目录，执行

	bundle install
程序为根据Gemfile的配置，自动安装所缺失的依赖项

安装完依赖项之后，继续执行

	bundle  exec jekyll server

待命令提示行显示

	Server running...press ctrl-c to stop.的时候，可以打开浏览器访问了http://127.0.0.1:4000/

# 四、搭建Linux部署环境 #

## 1、安装rvm ##

    gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
	curl -sSL https://get.rvm.io | bash -s stable
 
### 查看rvm安装路径 ###


    [root@bigdata-003 user]# find / -name rvm
	/usr/local/rvm
	/usr/local/rvm/scripts/rvm
	/usr/local/rvm/bin/rvm
	/usr/local/rvm/lib/rvm
	/usr/local/rvm/src/rvm
	/usr/local/rvm/src/rvm/scripts/rvm
	/usr/local/rvm/src/rvm/bin/rvm
	/usr/local/rvm/src/rvm/lib/rvm


发现在 /usr/local/rvm路径
并将/usr/local/rvm/bin添加到环境变量中

修改 RVM 的 Ruby 安装源到 Ruby China 的 Ruby 镜像服务器，这样能提高安装速度
echo "ruby_url=https://cache.ruby-china.com/pub/ruby" > /usr/local/rvm/user/db
这里的 > /usr/local/rvm/user/db 路径为上一步查找到的rvm路径下的user/db

## 2、Ruby 的安装与切换 ##

列出已知的 Ruby 版本

	rvm list known

安装一个 Ruby 版本（最新版）

	rvm install 2.6.0 --disable-binary

这里安装了最新的 2.6.0, rvm list known 列表里面的都可以拿来安装。
切换 Ruby 版本

	rvm use 2.6.0

如果想设置为默认版本，这样一来以后新打开的控制台默认的 Ruby 就是这个版本

	rvm use 2.6.0 --default

查询已经安装的ruby

	rvm list

卸载一个已安装版本（如果有的话）

	rvm remove 1.8.7

## 3、安装jekyll 

切换gem数据源 https://rubygems.org/ 国内被墙 需要更换成 https://gems.ruby-china.com/

注意：https://gems.ruby-china.com/ 这个国内的ruby源换过很多次，截至2019.5.1 只有这个是可以连接上的。

	gem sources --remove https://rubygems.org/
	gem sources -a https://gems.ruby-china.com/ 

查看gem数据源

	gem sources -l

	*** CURRENT SOURCES ***
	
	https://gems.ruby-china.com/

安装jekyll

	gem install jekyll

# 五、自定义域名 #

需要设置域名解析，将域名的地址指向自己的 github 博客地址。这里以万网的域名配置为例，选择需要设置的域名点击解析，在域名解析页面添加以下两条记录

![](http://www.nangongyibin.com/assets/images/blog1.png)

红框内，需要填写自己github_username值。

然后重新打开项目的 Settings > GitHub Pages 页面，Custom domain 下的输入框输入刚才设置的域名：xxx.com，点击保存即可。

![](http://www.nangongyibin.com/assets/images/blog2.png)

重新配置 _config.yml

打开项目目录下的 _config.yml 文件，修改以下配置：

	url: http://www.xxx.com

等待一分钟之后，浏览器访问地址：www.xxx.com 即可访问博客。


# 六、自动化部署 #

## 1、配置 Webhook ##

在 Github 仓库的项目界面，比如本博客项目 https://github.com/ityouknow/ityouknow.github.io，点击 Setting->Webhooks->Add Webhook，在添加 Webhooks 的配置信息，我的配置信息如下：

	Payload URL: http://www.ityouknow.com/deploy
	Content type: application/json
	Secret: 123456

如下图：


![](http://www.nangongyibin.com/assets/images/blog3.png)

## 2、服务器接受推送 ##

首先添加源

	sudo rpm -ivh https://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-11.noarch.rpm
	
	//yum安装node.js
	yum install -y nodejs

然后在安装 github-webhook-handler

	npm install -g github-webhook-handler     #安装 github-webhook-handler
	#如果没有安装成功，可以选择法2来安装
	npm install -g cnpm --registry=http://r.cnpmjs.org
	cnpm install -g github-webhook-handler

安装成功之后，我们需要添加一个脚本。进入到安装目录下：

	cd  /usr/lib/node_modules/github-webhook-handler

新建 deploy.js

	vi deploy.js

脚本内容如下：

	var http = require('http')
	var createHandler = require('github-webhook-handler')
	var handler = createHandler({ path: '/deploy', secret: 'ityouknow' }) //监听请求路径，和Github 配置的密码
	 
	function run_cmd(cmd, args, callback) {
	  var spawn = require('child_process').spawn;
	  var child = spawn(cmd, args);
	  var resp = "";
	 
	  child.stdout.on('data', function(buffer) { resp += buffer.toString(); });
	  child.stdout.on('end', function() { callback (resp) });
	}
	 
	http.createServer(function (req, res) {
	  handler(req, res, function (err) {
	    res.statusCode = 404
	    res.end('no such location')
	  })
	}).listen(3006)//监听的端口
	 
	handler.on('error', function (err) {
	  console.error('Error:', err.message)
	})
	 
	handler.on('push', function (event) {
	  console.log('Received a push event for %s to %s',
	    event.payload.repository.name,
	    event.payload.ref);
	  run_cmd('sh', ['/usr/local/depoly.sh'], function(text){ console.log(text) });//成功后，执行的脚本。
	})

脚本的作业就是启动一个监听端口来接收请求，接收到请求后执行部署脚本，脚本内容的关键点已经标注上注释。

部署博客的脚本如下：depoly.sh

	echo `date`
	cd /usr/local/ityouknow.github.io
	echo start pull from github 
	git pull http://github.com/ityouknow/ityouknow.github.io.git
	echo start build..
	jekyll build --destination=/usr/share/nginx/html


就是拉取代码，进行部署而已。

这个脚本的启动需要借助 Node 中的一个管理 forever 。forever 可以看做是一个 nodejs 的守护进程，能够启动，停止，重启我们的 app 应用。

不过我们的先安装 forever，然后需要使用 forever 来启动 deploy.js 的服务，执行命令如下：

	npm install forever -g   #安装
	$ forever start deploy.js          #启动
	$ forever stop deploy.js           #关闭
	$ forever start -l forever.log -o out.log -e err.log deploy.js   #输出日志和错误
	/root/node-v8.12.0-linux-x64/lib/node_modules/forever/bin/forever start -l forever.log -o out.log -e err.log deploy.js

同时一般情况下，我们不会对外保留很多端口，所以需要通过博客的地址来转发，需要在 Nginx 上面添加一个转发配置，用来监听的 /deploy 请求转发到 nodejs 服务上，配置代码如下：

	location = /deploy {
	     proxy_pass http://127.0.0.1:3006/deploy;
	}

这样我们整个自动化部署就完了，每次提交代码时，Github 会发送 Webhook 给地址http://www.ityouknow.com/deploy，Nginx 将 /deploy 地址转发给 Nodejs 端口为 3306 的服务，最后通过 github-webhook-handler 来执行部署脚本，已到达自动部署的目的。