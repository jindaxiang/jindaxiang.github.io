---
title: Python_s1_day02_topic_skills_Set_domestic_source
date: 2018-06-29 16:20:52
tags: [Skill]
categories: [Python]
---
# Set Python default domestic source
PIP安装源替换成国内镜像，可以大幅提升下载速度，还可以提高安装成功率。
If you always install packages from pypi, then you will find that use default source will be very slow!
you can use domestic source from the next list:

## Attention: new version ubuntu require https!

- 清华：https://pypi.tuna.tsinghua.edu.cn/simple
- 阿里云：http://mirrors.aliyun.com/pypi/simple/
- 中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
- 华中理工大学：http://pypi.hustunique.com/
- 山东理工大学：http://pypi.sdutlinux.org/ 
- 豆瓣：http://pypi.douban.com/simple/

# Temporary use
you can add parameters in pip install -i https://pypi.tuna.tsinghua.edu.cn/simple

for example: pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pyspider
you will download the pyspider from the TUNA source

# Permanent change
Under the environment of Linux, fix ~/.pip/pip.conf (没有就创建一个文件夹及文件。文件夹要加“.”，表示是隐藏文件夹)

content as follows：
```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host=mirrors.aliyun.com
```
Under the environment of windows, create the dir under the user dir, for example：C:\Users\xx\pip, create pip.ini。content as above.

<!--more-->