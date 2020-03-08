---
title: 'Cisco Administrative mode 与 Operational mode区别'
date: 2018-05-18 08:58:11
tags: 
- cisco
- 网络
categories: 网络
---
最近考NA，有道题目难到我，题目是这样的。
这里写图片描述
问题主要集中下C D 关于operationnal mode 和 administrator mode区别
百度在cisco论坛，看了不同的人回答。在这里总结一下。
# show interfaces switchport
<pre>
“# show interfaces switchport” command gives output of each and every port in the switch. For every switch port there are Two modes, which are Administrative Mode and Operational mode.

Administrative Mode: This mode denotes what we configure onto that particular port.. like Trunk or Access or LaGP or PaGP or ON and Administrative encapsulation etc…

Operational Mode: This mode is what a switch-port behaves in response to the configuration done onto a particular port.

For example.. if we configure Trunk on one switch port and on the other end on another switch, if we configure access.. how it behaves.. though it’s configured as trunk, it doesn’t work as a trunk. Here the “Administrative” mode is “Trunk”.. but “Operational” mode is “Access”.

Hope this is some informative. Thanks a lot.
</pre>

实际上也就是说 管理模式是我们配置的模式 但是实际工作模式是不一样的 在packet tracer里面 输入show interfaces switchport
例如一个 没启动的端口显示如下
Administrative Mode: dynamic auto
Operational Mode: down