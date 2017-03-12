# tjlnotes.github.io
study notes
#### 安装hexo
1. 全局安装hexo：
打开命令行，输入：
```
$ npm install -g hexo
```
2. 初始化hexo项目

打开需要将hexo项目存放的目录，例如我存放在的D盘下的workspace文件夹。在此文件夹下创建一个新文件夹下，可取名为“blog”，进入blog文件夹，
`Shift + 鼠标右键`在此处打开命令行窗口，输入指令：
```
$ hexo init
```
等待安装完成
3. 安装项目依赖包
```
$ npm install
```
4. 构建页面并运行hexo本地服务，查看是否安装正确
```
$ hexo clean
$ hexo generate
```
等待构建完成后，运行本地服务
```
$ hexo server
```
出现以下提示则服务启动成功，可打开浏览器并输入[localhost:4000](http://localhost:4000)查看原始博客页面
```
$ hexo server
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
```

注：由于在Hexo 3.0 后server被单独出来了，所以若server命令报错或无反应，可通过命令安装server模块：
```
$ npm install hexo-server --save
```

## 配置github并接通hexo
1. 建立Repository
创建github账号，并建立与你用户名对应的仓库，仓库名必须为【your_user_name.github.io】，固定写法
2. 配置ssh
使用git提交和下载代码时总共有两种协议，https和ssh。此处我是用的是ssh，也可根据个人偏好使用https。
使用ssh协议时的配置如下：

2.1. 检查本机是否有ssh key设置

右键打开git bash
```
$ cd ~/.ssh
```
如果没有则提示：No such file or directory
没有则进入~/.ssh路径下

2.2. 使用git bash生成新的ssh key
```
$ cd ~                                       ----保证当前路径在"~"下
$ ssh-keygen -t rsa -c "xxxxxx@yy.com"       ----填写注册github时使用的邮箱地址
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/xxxx_000/.ssh/id_rsa):   ----不填直接回车
Enter passphrase (empty for no passphrase):   #输入密码（可以为空）
Enter same passphrase again:   #再次确认密码（可以为空）
Your identification has been saved in /c/Users/xxxx_000/.ssh/id_rsa.   ----生成的密钥
Your public key has been saved in /c/Users/xxxx_000/.ssh/id_rsa.pub.   ----生成的公钥
The key fingerprint is:
e3:51:33:xx:xx:xx:xx:xxx:61:28:83:e2:81 xxxxxx@yy.com
```
本机已完成ssh key设置，其存放路径为：c:/Users/xxxx_000/.ssh/下。

 2.3. 添加ssh key到github

 a. 登录GitHub系统；点击右上角账号头像的“▼”→Settings→SSH kyes→Add SSH key。
 b. 进入c:/Users/xxxx_000/.ssh/目录下，打开id_rsa.pub文件，全选复制公钥内容。
 c. Title自定义，将公钥粘贴到GitHub中Add an SSH key的key输入框，最后“Add Key”。

 ![](../img/sshkey.jpg)

 d. 测试ssh keys是否设置成功。
 ```
 $ ssh -T git@github.com
 Hi tjlnotes! You've successfully authenticated, but GitHub does not provide shell access.
 ```

3. 配置hexo
找到博客根目录下的_config.yml文件，用记事本打开，并将最后几行改成
```
deploy:
  type: git
  repo: git@github.com:tjlnotes/tjlnotes.github.io.git
  branch: master
```
注意，repo后接自己的github仓库地址（在建立完仓库后可从个人的repository查看到）。
如果使用的是ssh协议，此处填ssh地址，如果使用https协议此处就填https地址。

4. 安装hexo-deployer-git模块
此目录下打开命令行键入
```
$ npm install hexo-deployer-git --save
```

5. 重新构建页面并发布到github上
```
$ hexo clean
$ hexo generate
$ hexo deploy
Branch master set up to track remote branch master from git@github.com:tjlnotes/
tjlnotes.github.io.git.
To github.com:tjlnotes/tjlnotes.github.io.git
 + cd219d1...d275f0d HEAD -> master (forced update)
INFO  Deploy done: git
```
发布成功，就可以打开个人主页查看效果了[http://yourgithubname.github.io](https://tjlnotes.github.io/)

每次编辑博客后都由这三个命令进行构建和发布

### 参考
- [在Windows平台上安装Node.js及NPM模块管理](http://www.cnblogs.com/seanlv/archive/2011/11/22/2258716.html)
- [【看云】nvm，nodejs和npm安装使用](http://www.kancloud.cn/summer/nodejs-install/71975)
- [【简书】HEXO+Github,搭建属于自己的博客](http://www.jianshu.com/p/465830080ea9)
- [【知乎】有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335)
- [【百度经验】window下配置SSH连接GitHub、GitHub配置ssh key](http://jingyan.baidu.com/article/a65957f4e91ccf24e77f9b11.html)
- [NexT主题使用文档](http://theme-next.iissnan.com/)
