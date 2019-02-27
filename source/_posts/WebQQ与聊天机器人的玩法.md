---
date: 2017-06-06 23:06:19
status: public
title: WebQQ与聊天机器人的玩法
keywords: 
- Python 
- QQ
- 聊天
- 机器人
tags:
- Python 
- QQ
- 聊天
- 机器人
categories: 好玩
 
---


# QQ小黄鸡VPS挂机版

[![Build Status](https://travis-ci.org/zeruniverse/QQRobot.svg?branch=master)](https://travis-ci.org/zeruniverse/QQRobot)
[![Code Health](https://landscape.io/github/zeruniverse/QQRobot/master/landscape.svg?style=flat)](https://landscape.io/github/zeruniverse/QQRobot/master)
![Release](https://img.shields.io/github/release/zeruniverse/QQRobot.svg) 
![Environment](https://img.shields.io/badge/python-2.6%2C%202.7-blue.svg) 
![License](https://img.shields.io/github/license/zeruniverse/QQRobot.svg) 

该项目修改自SmartQQBOT这一项目，支持在VPS下nohup命令挂机。QQ协议说明请参考原项目。

请帮忙分析Android QQ协议：此项目现已稳定，在更新协议前不会有大更新。希望有人能跟我一起搞手机QQ协议，SmartQQ协议稳定性不是很理想。

重要：群聊被TX认为是极度危险的行为，因此如果账号被怀疑被盗号（异地登陆），群聊消息会发不出去。表现为程序能收到群聊消息，群聊消息发送返回值为发送成功，但其他群成员无法看到您发出的消息。大约登陆10分钟后您会收到QQ提醒提示账号被盗，要求改密码，同时账号被临时冻结。不知为何该程序刚运行时总是被怀疑异地登陆，当您重复解冻3次后（就是改密码），TX基本就不再怀疑您了，一般一次能稳定挂机2-3天。强烈推荐您用小号挂QQ小黄鸡！

This project is a chatting robot in QQ, implemented in Python. The robot uses Artificial Intelligent API to generate response. QQ is a popular instant chatting service in China, which is similar to Facebook Messenger. The robot supports group chatting and private chatting and should be only used for fun.

Here is a similar project used to keep QQ account online with the function to record messages and forward to your E-mail.


登陆时采用QQ安全中心的二维码做为登陆条件, 不需要在程序里输入QQ号码及QQ密码。QQ自动回复私聊（无群聊功能）及留言邮件提醒版本请看这里。


## 如何使用

从http://www.tuling123.com/openapi/ 申请一个API KEY(免费，5000次/天)， 贴到QQBot.py的第36行 (测试KEY：c7c5abbc9ec9cad3a63bde71d17e3c2c)
修改groupfollow.txt,将需要小黄鸡回复的群的群名写入(小黄鸡必须为群成员),每行一个群名，请不要打多余的空格。（新版WEBQQ已移除获取群号的接口，输入中文群名请务必使用UTF-8编码）
nohup python2 QQBot.py >qbot.log&
ls
若出现v.png则用QQ安全中心扫描，否则继续ls
cat log.log可以输出运行LOG
强烈建议使用小号挂小黄鸡，已知QQ会临时封禁机器人的临时对话回复和群回复，原理未知，每次封禁约为10分钟。表现为发送消息返回值retcode 为 0 但其他人无法看到。长时间挂机会导致QQ被冻结错误，QQ安全中心提示发布不良信息
据反馈此AI平台回复中带有少量广告。。。(如问iphone6价格回复小米799)
功能

注：以下命令皆是在QQ中发送，群聊命令发送到所在群中

关于及帮助，在群聊中发送!about

群聊智能回复，在群中通过发送!ai 问题语句，则机器人向AI平台请求问题的回复并回复到群，带有!ai关键字时优先触发此功能

私聊智能回复，对于收到的私聊，机器人向AI平台请求该聊天记录的回复并回复给消息发送者

群聊学习功能，类似于小黄鸡，在群中通过发送!learn {ha}{哈哈}语句，则机器人检测到发言中包含“ha”时将自动回复“哈哈”。!delete {ha}{哈哈}可以删除该内容。学习内容会自动储存在database.群号.save文件。!deleteall可删除该群所有记录。注意learn和{之间有空格，{}与{}之间没有。

群聊复读功能，检测到群聊中连续两个回复内容相同，将自动复读该内容1次。

群聊关注功能，使用命令!follow {QQ昵称}!可以使机器人复读此人所有发言（除命令外）使用命令!unfollow {QQ昵称}!解除关注。例如 !follow 卖火柴的小女孩!。{QQ昵称}处可使用"me"来快速关注与解除关注自己，例：!follow me!

私聊直接聊天即可，不需要加任何前缀。


## Refs
https://github.com/b3log/xiaov

- https://github.com/ScienJus/smartqq/wiki/%E7%99%BB%E5%BD%95-Api
- http://www.scienjus.com/webqq-analysis-2/