---
title: Install OS in Deeping Learning Machine
date: 2019-09-14 18:00:52
tags: [Record]
categories: [System]
---

# 深度学习服务器重装系统记录

## 配置介绍
1. CPU: E5 2620 V4
2. Memory: 100G
3. Nvidia: 1080Ti * 2

## 安装系统
1. 下载UltralISO试用版：https://cn.ultraiso.net/
2. 安装
3. 下载win10最新镜像：https://msdn.itellyou.cn/
4. 打开UltralISO，点击-继续试用
5. 文件-打开-win10镜像的路径
6. 启动-写入硬盘镜像
7. 模型参数 HDD+
8. 注意U盘会被格式化，写入很快，记得用指定U盘，有些识别不了
9. 因为默认格式化会用Fat32格式，不支持大于4G的文件，所以需要调整
10. 此时 cmd 打开，输入：convert f: /fs:NTFS （F盘为我的U盘所在盘符）
11. 解压打开镜像文件，找到Sources目录下的install.wim文件，复制到对应的U盘目录下。
12. U盘安装制作完成
13. 在系统BIOS选择DUAL 或者 UEFI 都可以，模型UEFI启动，速度快，支持2T以上硬盘，参考：http://baijiahao.baidu.com/s?id=1596082869749554401&wfr=spider&for=pc
14. 关于硬盘分区：https://zhidao.baidu.com/question/2056165228240621947.html
15. 安装如下必须软件
- Office 2019
- Notepad++
- Pycharm pro
- Anaconda3
- 7zip
- 迅雷，取消自动
- 百度云盘

