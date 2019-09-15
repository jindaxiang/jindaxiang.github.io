---
title: Python_basic
date: 2019-09-15 18:00:52
tags: [Record]
categories: [Python]
---

```python
# coding=utf-8
# /usr/bin/env python
"""
Author: Albert King
date: 2019/9/15 18:27
desc: 调用 configparser 模块管理您的 token，防止重要信息外泄；调用 pathlib 模块管理路径；利用 f-strings 管理字符串替换
"""
from pathlib import Path  # 路径管理模块
import logging  # 日志管理模块

import configparser  # 配置管理模块
import jqdatasdk as jq  # 聚宽数据接口
import tushare as ts  # Tushare 数据接口

logger = logging.getLogger()
logger.setLevel(logging.INFO)
logFormatter = '%(asctime)s - %(user)s - %(levelname)s - %(message)s'
formatter = logging.Formatter(fmt=logFormatter)

console = logging.StreamHandler()  # 配置日志输出到控制台
console.setLevel(logging.INFO)  # 设置输出到控制台的最低日志级别
console.setFormatter(formatter)  # 设置格式
logger.addHandler(console)

handler = logging.FileHandler('king.log', mode='w')  # mode="a", 为追加文件; mode="w", 为擦出后写入文件
handler.setLevel(logging.INFO)
handler.setFormatter(formatter)
logger.addHandler(handler)
logger.info("Begin record", extra={'user': 'king'})


path_ini = Path(r'account_info.ini')
config = configparser.ConfigParser()
config.read(path_ini)
jq_username = config['joinquant']['username']
jq_password = config['joinquant']['password']

jq.auth(jq_username, jq_password)
jq.get_all_securities()
ts_token = config['tushare']['token']
pro = ts.pro_api(ts_token)


data = pro.stock_basic(exchange='', list_status='L', fields='ts_code,symbol,name,area,industry,list_date')

for item in data['ts_code'][:10]:
    temp_df = pro.daily(ts_code=item, start_date='20180701', end_date='20180718')
    temp_df.to_csv(f'{item}.csv')
    logger.info(f"{item} finished", extra={'user': 'king'})


my_name = "jindaxiang"
logger.info(f"Finished by {my_name.upper()}", extra={'user': 'daxiang'})


with open('king.log', 'r') as f:
    print(f.read())
```

