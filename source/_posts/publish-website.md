---
title: How to publish my personal website on coding.net
date: 2020-06-24 16:09:52
tags: [Website]
categories: [Website]
---

# How to publish my personal website on coding.net

## Login Page

jindaxiang.coding.net

## Find Item

项目 -> jindaxiang -> 持续部署 -> 静态网页 -> 设置 -> 自定义域名 -> Warning -> 申请 -> 在阿里云重启 GitHub 的解析

## Warning

阿里云 -> 域名 -> 解析 -> 暂停 GitHub 的解析

## Frequency

每月一次

## Attention

If you are old customer of coding.net, so you have to update **_config.yml** file with conding site object

## bind www.jfds.xyz

1. 先在阿里云添加主机记录，按照 coding 绑定 www.jfds.xyz 域名那块的提示
2. 再次绑定 www.jfds.xyz 域名
3. Https 勾选 -> 保存 -> 部署网站
