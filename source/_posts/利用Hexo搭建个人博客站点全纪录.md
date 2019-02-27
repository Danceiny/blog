---
date: 2017-05-13 15:51:03
status: public
title: 利用Hexo搭建个人博客站点全纪录
keywords: 
- Hexo
- 入门
- 教程
- 博客
- blog
- 个人博客
tags: 
- 个人网站
- 博客
- 教程
categories: DOSOMETHING
 
---

# 需求澄清
- 个人博客。
- 静态的即可。
- 可由GitHub Pages或者Coding.net Pages服务托管。
- 要有域名，好记。
- 博客中有图片，需要稳定的存储。
- 维护与操作系统平台无关（因为自己各种操作系统切换）。

# 技术选型
Hexo + GitHub/Coding Pages双托管 + 腾讯云解析 + 七牛云图片存储

# 开始配置

## 安装Hexo
首先安装npm，使用npm安装hexo。
- [npm](https://www.npmjs.com/)
- [Hexo](https://hexo.io/zh-cn/)


## 主题Next
安装：http://theme-next.iissnan.com/getting-started.html

## GitHub
仓库地址：https://github.com/Danceiny/blog
Pages地址：https://danceiny.github.io/blog
添加CNAME文件，指向blog.cannot.cc，Pages地址重定向到该域名。



## Coding
同上。

## 腾讯云解析
已有域名（已备案）: [cannot.cc](http://cannot.cc)

添加二级域名: [blog.cannot.cc](http://blog.cannot.cc)

添加CNAME类型的记录，记录值设置为danceiny.github.io.

把www.blog.cannot.cc记录到pages.coding.me.

顺便把cannot.cc解析到 http://danceiny.github.io 了。（原来在Github上的个人主页）。有空再修改。

注意：
1. 腾讯云解析的记录值是比较需要关注的。
2. www是个神奇的东西，http://blog.cannot.cc 和 http://www.blog.cannot.cc 是不一样的两个东西。

## 七牛图床
https://portal.qiniu.com/bucket/
有很多官方工具可以使用，命令行，GUI，但是目前我感觉不太用户友好。访问秘钥就是两个：Access Key和Secret Key。Bucket像是GitHub里的仓库吧，我叫它**对象存储仓库**。


## 阅读次数统计
1. 可在Next中配置，使用leancloud.cn [参见博客](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%8)


## 社交分享
直接在Next中开启jiathis即可。不支持https是个隐患。

## 站点搜索
可选的几个服务都是收费的，所以我选了本地的搜索。按照Next的教程配置即可。

## 百度联盟
http://union.baidu.com
申请，未通过，网站内容还是少了点。

## 百度统计
站点访问统计。百度统计的账号和百度联盟账号可以不一样，不过还是统一账号比较好，方便管理。

## 谷歌分析


## 跟帖回复评论
使用Facebook的评论系统。

网易云跟帖未引入，不过看起来效果不错。


## SEO
1.	Hexo优化之为外部链接添加nofollow  https://liuzhichao.com/2016/hexo-auto-nofollow.html

2.	https://eason-yang.com/2016/08/03/tips-for-hexo-and-hexo-next/

3. [hexo高阶教程：教你怎么让你的hexo博客在搜索引擎中排第一](https://juejin.im/post/590b451a0ce46300588c43a0)

## 站点地图
通过npm下载插件。有专门针对百度的。可做SEO。

sitemaps.xml

## RSS订阅
通过npm下载插件。


## Facebook Audience广告投放
未搞定。

## Hexo部署
https://hexo.io/docs/deployment.html

可部署到百度，方便搜索引擎收录。


## CNAME覆盖问题
https://www.stayhungry.me/2015/07/26/%E6%90%AD%E5%BB%BAHexo%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9/


## 利用分支备份Hexo项目源代码
在博客对应的GitHub项目上创建Hexo分支。Pages服务用的是master分支。

yaml重要配置文件不应该上传到公开项目。


## 去掉post的url中的日期
permalink: :title.html

## 其他优秀的同类型博客
http://litten.me/



