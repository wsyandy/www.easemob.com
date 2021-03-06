---
title: 入门指南
secondnavgettingstart: true
sidebar: gettingstartsidebar
---

![alt text](/chat_nick.png "昵称和头像的获取和显示流程")
<br/><br/>
<h3>方法一 从APP服务器获取昵称和头像

<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;昵称和头像的获取：当收到一条消息（群消息）时，得到发送者的用户ID，然后查找手机本地数据库是否有此用户ID的昵称和头像，如没有则调用APP服务器接口通过用户ID查询出昵称和头像，然后保存到本地数据库和缓存，下次此用户发来信息即可直接查询缓存或者本地数据库，不需要再次向APP服务器发起请求</p>
	
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;昵称和头像的更新：当点击发送者头像时加载用户详情时从APP服务器查询此用户的具体信息然后更新本地数据库和缓存。当用户自己更新昵称或头像时，也可以发送一条透传消息到其他用户和用户所在的群，来更新该用户的昵称和头像。</p>

<h3>方法二 从消息扩展中获取昵称和头像

<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;昵称和头像的获取：把用户基本的昵称和头像的URL放到消息的扩展中，通过消息传递给接收方，当收到一条消息时，则能通过消息的扩展得到发送者的昵称和头像URL，然后保存到本地数据库和缓存。当显示昵称和头像时，请从本地或者缓存中读取，不要直接从消息中把赋值拿给界面（否则当用户昵称改变后，同一个人会显示不同的昵称）。</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;昵称和头像的更新：当扩展消息中的昵称和头像URI与当前本地数据库和缓存中的相应数据不同的时候，需要把新的昵称保存到本地数据库和缓存，并下载新的头像并保存到本地数据库和缓存。</p>

<h3>昵称或头像处理的方法一和方法二区别：<br>

方法一：在发送消息时不含有任何扩展，收消息时如果本地不存在发送人的用户信息则需要从APP服务器查询发送人的昵称和头像的URL。<br/><br/>
方法二：在发送消息时带有包含昵称和头像URL的消息扩展，收到消息时即可从消息扩展中取出，不需要再去APP服务器获取，

方法二和方法一相比<br/>
<strong>优点</strong>：收到消息立即显示昵称不用等待APP服务器返回数据后显示。<br/>
<strong>缺点：</strong>每条消息都要带有扩展，增加消息体积，每次发消息都有一些不必要的数据。