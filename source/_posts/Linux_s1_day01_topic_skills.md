---
title: 	Linux_s1_day01_topic_skills
date: 2018-06-19 16:09:52
tags: [Skill]
categories: [Linux]
---
# common characters
- [*] 匹配零个或多个字符
- ? 匹配任意一个字符
- [0-9] 匹配一个数字范围
- [abc] 匹配列表里的任何字符
- [^abc] 匹配列表以外的字符

# search command
- ctrl+r 命令搜索

# su methods
- su - 切换为root用户，启用一个全新的终端
- su 仅切换用户身份不切换终端
- id 显示当前用户信息
- passwd 修改当前用户密码
- 命令后添加&在后台运行该进程
- ctrl+z暂停某个程序
- jobs显示后台运行的程序
- bg[id]使id指定的程序继续在后台运行
- fg[id]使id指定的程序调回前台工作
- touch 创建一个空白文件或者更新已有文件的时间
- ls -a 显示所有文件
- ls -l 显示详细信息
- ls -R 递归显示子目录结构
- ls -ld 显示目录和连接信息
- file 查看文件的类型
- cd.. 上一个目录
- cd . 当前目录
- cd ~ 用户的家目录
- cd - 上一个工作目录
- cp -r 源文件（文件夹）目标文件（文件夹）递归复制整个目录树
- cp -v 源文件（文件夹） 目标文件（文件夹）显示复制详细信息
- mv 文件 目标目录 移动文件或目录，如果指定文件名，则可以重命名文件
- rm filename 删除文件
- rm -r 删除目录及其中的所有内容
- rm -i 交互式删除
- rm -f 强制删除，没有警告提示
- mkdir 创建一个目录
- rmdir 删除一个空目录
- rm -r 删除一个非空目录
- date 查看、设置当前系统时间
- hwclock(clock) 用以显示硬件时钟时间
- cal 查看日历
- uptime 查看系统运行时间
- echo 显示输入的内容
- cat 显示文件内容
- head 显示文件头几行，默认10行，-n指定显示的行数
- tail 显示文件末尾的几行，默认10行，-n指定显示的行数 -f 追踪显示文件更新
- more 翻页显示文件内容，只能向下翻页
- less 翻页显示文件内容，带上下翻页
- lspci 查看PCI设备，-v查看详细信息
- lsusb 查看USB设备，-v查看详细信息
- lsmod 查看加载的驱动（模块）
- shutdown -h now 立即关机
- shutdown -h +10 10分钟后关机
- shutdown -h 23：00 23：00分关机
- shutdown -r now 立即重启，也可定时关机
- poweroff 立即关机
- reboot 立即重启
- zip *.zip filename 压缩文件
- unzip *.zip 解压缩文件
- gzip filename 压缩文件
- gzip -d *.gz 解压缩文件
- tar -cvf *.tar filename 归档文件，不压缩
- tar -xvf *.tar 释放归档文件
- tar -cvzf *.tar.gz filename -z参数将归档后的归档文件进行gzip压缩
- locate filename 快速查找文件、文件夹，此命令需要预先建立数据库，updatedb命令手工建立、更新数据库
- find 查找位置，查找参数
- find .-name *linux*查找当前目录下包含linux的文件
- find / -perm 777 查找根目录下权限为777的文件
- find / -type d 查找根目录下类型为目录的文件
- find / -name a* -exec ls -ls {} 查找以a开头的文件并执行ls -l命令，-exec{}; 为固定格式
- vim
- :x 保存并退出
- :!系统命令 执行一个系统命令
- :sh 切换到命令行，使用ctrl+d切换回vim