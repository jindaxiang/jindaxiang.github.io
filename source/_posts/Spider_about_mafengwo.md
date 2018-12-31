---
title: Spider_about_mafengwo
date: 2018-10-24 10:09:52
tags: [Skill]
categories: [Spider]
---

# Introduction
During the National Day Holidays, i did some work for the purpose of writing a repot about Mount Emei scenic area. The first thing i want to do is how to get the information about Mount Emei, when i was browsing websites on internet, Mafengwo come into my eyes. Then i will pay more attention on mafengwo, especially about how to fetch the data of hotels in every scenic area in www.mafengwo.com
# Step one
Firstly, i will open the chrome broswer and type in the website of our objective. www.mafengwo.com, then click the http://www.mafengwo.cn/mdd/ site, you will see the ![pic_1](http://p659fi1z8.bkt.clouddn.com/pic_1.jpg), our destination is the Mount Emei, so i click the 峨眉山, then we get into http://www.mafengwo.cn/travel-scenic-spot/mafengwo/10143.html, yes, it's the website we needed. In the process of fethcing the data, i think that, to fetch the hotel data is the most difficult, so i choose this part to do a favor. You should broswer the http://www.mafengwo.cn/hotel/10143/?sFrom=mdd, and you will find it's something interesting there, because the price of hotle is shown on the screen.
# Step two
Click the right button of mounse, open the check, then go to the network tab, press the preserver log item, just as follows:
then you should reload the website, go into the source tab and press top, right click the top button, choose search in all files, then input 'getSign', just as ![pic_2](http://p659fi1z8.bkt.clouddn.com/pic_2.jpg). Use the debuger function of chrome. You can find the return value, it's md5 encryption, use the dict and str content to generate the salt, then use get method to transmit the parameters to host.

