---
title: 在 Hexo 中插入 Chart 动态图表
date: 2020-09-10 14:09:52
tags: [Hexo]
categories: [JavaScript]
---

# Reference

[Visit here](https://shen-yu.gitee.io/2020/chartjs/)

# Demo here

{% chart 90% 300%}
    {
    type: 'line',
    data: {
    labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
    datasets: [{
        label: 'My First dataset',
        backgroundColor: 'rgb(255, 99, 132)',
        borderColor: 'rgb(255, 99, 132)',
        data: [0, 10, 5, 2, 20, 30, 45]
        }]
    },
    options: {
        responsive: true,
        title: {
        display: true,
        text: 'Chart.js Line Chart'
        }
    }
    }
{% endchart %}
