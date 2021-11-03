---
title: 搭建Github Pages博客
index_img: https://avatars2.githubusercontent.com/t/3419353?s=280&v=4
categories: Hexo+Github Pages博客
tags: 
    - Hexo博客搭建
    - Docker  
excerpt: 本文是在Windows 10上创建docker容器（Hexo构建环境），之后用VS Code连接Docker容器进行博客创作，利用Github Action监听git push事件，实现一键构建博客页面
---

本文是在Windows 10上创建docker容器（Hexo构建环境），之后用VS Code连接Docker容器进行博客创作，利用Github Action监听git push事件，实现一键构建博客页面

## **一、注册Github账号**

1. 用浏览器打开<a class="btn" href="https://github.com/github" title="https://github.com/github">Github官网</a>,如下图所示，点击Sign up按钮；

![Github官网](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/01Github官网.png)

2. 然后依次填写用户名、邮箱和密码，如下图所示，点击Create account按钮；

![Github注册界面](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/02Github注册界面.png)

3. 主要是选择注册账号的目的及你所擅长的开发语言，可以什么都不选，直接跳过，滚动到页面底部，如下图所示，点击Complete setup按钮；

![注册Github的目的](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/03注册Github的目的.png)

4. 验证邮箱地址；

![Github邮箱认证](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/04Github邮箱认证.png)

5. 登录注册时的邮箱，查看noreply@github.com发送的邮件，如下图所示，点击Verify email address按钮；

![Github注册邮箱认证](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/05Github注册邮箱认证.png)

## **二、创建Github仓库**

1. 创建仓库，如下图所示，点击Create a repository按钮；

![创建Github仓库](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/06创建Github仓库.png)

2. 创建仓库，仓库的名称与用户名保持一致，如下图所示，点击Create repository按钮；

![设置Github仓库参数](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/07设置Github仓库参数.png)

3. 点击Setting按钮；

![设置Github仓库](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/08设置Github仓库.png)

4. 在该页面底部附近，如下图所示，点击None按钮，选择分支名称，这里直接选择main；

![设置Github Pages显示分支](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/09设置Github%20Pages显示分支.png)

5. 点击按钮Choose a theme；

![设置Github Pages主题](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/10设置Github%20Pages主题.png)

6. 根据自己的喜好，选择主题，选完之后点击Select theme按钮；

![选择Github Pages主题](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/11选择Github%20Pages主题.png)

7. 进行初次提交；

![Github仓库初次提交](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/12Github仓库初次提交.png)

8. 根据自己的用户名，在浏览器的地址栏中输入https://${Github_User}.github.io，显示效果如下图所示；

![Github Pages初次效果展示](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/13Github%20Pages初次效果展示.png)

## **三、创建hexo构建环境**

1. 通过下面的命令进行构建docker容器；

```bash
docker build https://github.com/wenchengji159357/Hexo-blog-docker.git --file Dockerfile --build-arg Github_User="syedndeliar23602" --build-arg Github_Email="syedndeliar23602@gmail.com" --build-arg Github_Branch_Name="main" --tag hexo-blog-image
```

<p class="note note-primary">注：syedndeliar23602、syedndeliar23602@gmail.com修改成自己的GitHub用户名和GitHub邮箱，Github_Branch_Name为Github Pages设置的分支名称，默认为master，如果分支名称是master，则删除参数--build-arg Github_Branch_Name="main"即可，默认的博客主题是fluid</p>

2. 通过下面的命令拉取docker容器，并进入镜像；

```bash
 docker run -it hexo-blog-image -p 4000:4000 /bin/bash
```

3. 在浏览器的地址栏中输入http://localhost:4000， 显示效果如下图所示；

![Hexo blog本地效果展示](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/14Hexo%20blog本地效果展示.png)

4. 进入刚刚拉取的容器，输入以下命令查看SSH公钥，复制输出结果；

```bash
cat ~/.ssh/id_rsa.pub
```

5. 再次用浏览器打开<a class="btn" href="https://github.com/github" title="https://github.com/github">Github官网</a>，如下图所示，头像旁边的小三角，点击Settings按钮；

![打开Github账户设置](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/15打开Github账户设置.png)

6. 点击SSH and GPG keys按钮；

![添加SSH公钥](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/16添加SSH公钥.png)

7. 点击New SSH key按钮；

![添加SSH Key](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/17添加SSH%20Key.png)

8. 在Title下面的文本框中自己的实际情况进行命名，在Key下面的文本框中粘贴刚才的输出结果（SSH公钥），然后点击Add SSH key按钮；

![添加SSH Key内容](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/18添加SSH%20Key内容.png)

9. 在刚才的容器终端中，输入以下命令查看SSH私钥（用于Github Actions），复制输出结果；

```bash
cat ~/.ssh/id_rsa
```

10. 点击Setting按钮；

![设置Github仓库](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/19设置Github仓库.png)

11. 点击Secrets按钮和New repository secret按钮；

![新增secret](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/20新增secret.png)

12. 在Name下面的文本框中输入SSH_PRIVATE，在Value下面的文本框中粘贴刚才的输出结果（SSH私钥），然后点击Add secret按钮；

![添加SSH私钥](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/21添加SSH私钥.png)

13. 在刚才的容器终端中，输入以下命令，目的是把用于构建博客的代码上传至hexo_blog分支；

```bash
git push -u origin hexo_blog
```

14. 根据自己的用户名，在浏览器的地址栏中输入https://${Github_User}.github.io, 显示效果如下图所示；

![Hexo blog最终效果展示](https://gitee.com/wenchengji/images/raw/master/搭建Github%20Pages博客/22Hexo%20blog最终效果展示.png)
