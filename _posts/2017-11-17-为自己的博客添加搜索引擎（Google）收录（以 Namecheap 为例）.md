---
layout: post
title: 为自己的博客添加搜索引擎（Google）收录（以 Namecheap 为例）
date: 2017-11-17 15:40:11.000000000 +09:00
tags: Jekyll
---
博客搭好了，怎样才能让别人通过 Google 搜索到自己的博客呢？
下面，我们来看一下具体步骤。

#### Step 1：进入 Google 的 WebMaster 工具管理页面
- 进入[Search Control - 首页](https://www.google.com/webmasters/tools/home)页面，点击右上角**添加属性**。在这里，我们把需要收录的页面 url 填入。  
![1](http://ozjtrx3vo.bkt.clouddn.com/2017-11-17-1-2.jpeg)


- 点击**添加**后，跳到如下页面：  
![2](http://ozjtrx3vo.bkt.clouddn.com/2017-11-17-2-1.jpeg)


#### Step 2：进入 Namecheap.com，添加 TXT 记录。
- 登陆之后，点 **MANAGE**。
  ![3](http://ozjtrx3vo.bkt.clouddn.com/2017-11-17-3-1.jpeg)

- 进入管理页面后，点击右边的 **Advanced DNS**。然后点击下方 **ADD NEW RECORD**。
  ![4](http:////ozjtrx3vo.bkt.clouddn.com/2017-11-17-4-1.jpeg)

- 添加新的记录，类型选 **TXT Record**，Host 填 **@**，Value 填入 Step 1 中的字符串。
  ![5](http:////ozjtrx3vo.bkt.clouddn.com/2017-11-17-5-1.jpeg)


#### Step 3：在 Google Search Console 页面上点**验证**。
- 我们会看到如下页面：
  ![6](http:////ozjtrx3vo.bkt.clouddn.com/2017-11-17-6-1.jpeg)


#### Step 4：获得 sitemap 文件
- 进入 [XML-Sitemaps.com Sitemap Generator](https://www.xml-sitemaps.com/) 页面，输入博客地址，点击 **start**。
  ![7](http://ozjtrx3vo.bkt.clouddn.com/2017-11-17-7-2.jpeg)

- 等待搜索完成，点击 **VIEW SITEMAP DETAILS**。
  ![8](http://ozjtrx3vo.bkt.clouddn.com/2017-11-17-8-1.jpeg)

- 下载 SITEMAP 文件并将其放入网站的根目录。

#### Step 4：在 Google Search console 中添加你的 sitemap URL。
- 打开 Step 1 中的 [Google Search console](https://www.google.com/webmasters/tools/home) 网站，添加你的 sitemap URL。在这里，我的 sitemap URL 为：`http://gracegreat1.me/sitemap.url`。（因为上一步中已经将该文件放入网站的根目录）
![9](http:////ozjtrx3vo.bkt.clouddn.com/2017-11-17-9-1.jpeg)


#### 参考链接
- [Namecheap：验证您的域名](https://support.google.com/a/answer/6142985?hl=zh-Hans)<br>
- [了解站点地图](https://support.google.com/webmasters/answer/156184?hl=zh-Hans&ref_topic=4581190)<br>
- [利用github-pages建立个人博客](https://www.ezlippi.com/blog/2015/03/github-pages-blog.html)<br>
- [使用 Jekyll 搭建 Blog](https://jin-yang.github.io/post/jekyll.html)


