---
title: "Linux"
date: 2023-04-17T10:18:00+08:00
draft: false
---

##  添加域名映射：

sudo vim /etc/hosts  

## 无法正常登录：
1. 选择启动时，对着启动的内核摁e,对内核界面进行编辑，在linux16那一行的最后添加 init=/bin/sh	

2. 然后按ctrl +x。就进入救援模式，也称单用户模式。 

3. 系统此时是只读模式，改成读写模式执行如下命令:mount -o remount,rw /

4. 修改/etc/sysconfig/selinux    vim /etc/sysconfig/selinux

5. 改为SELINUX=disable  



## 常用命令

#### grep命令	
* grep命令用于查找文件里符合条件的字符串或者正则表达式。
* grep [options] pattern [files]

#### wc命令
* wc用于计算字数，可以计算文件的字节数，字数，或者列数
* 知道名称，或者文件名为“—”，则从标准输入设备读取数据
