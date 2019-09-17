---
title: Python_get_bond_data
date: 2019-09-17 22:00:52
tags: [Report]
categories: [Python]
---
```python
# coding=utf-8
# /usr/bin/env python
"""
Author: Albert King
date: 2019/9/13 22:48
desc: 获取中国银行间市场交易商协会(http://www.nafmii.org.cn/)中孔雀开屏(http://zhuce.nafmii.org.cn/fans/publicQuery/manager)
的债券基本信息数据
"""
from pathlib import Path

import pandas as pd
import requests

# 页面分析后获得的接口地址
obj_url = "http://zhuce.nafmii.org.cn/fans/publicQuery/releFileProjDataGrid"
# 添加游览器伪装
headers = {
    "Accept": "application/json, text/javascript, */*; q=0.01",
    "Accept-Encoding": "gzip, deflate",
    "Accept-Language": "zh-CN,zh;q=0.9,en;q=0.8",
    "Connection": "keep-alive",
    "Content-Length": "95",
    "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8",
    "Cookie": "Hm_lvt_508be7db52fd6da009f33b1d6a262bd3=1568385898; Hm_lpvt_508be7db52fd6da009f33b1d6a262bd3=1568385898; JSESSIONID=cEArLxkgwPfryBR_dAOfQEXfKx2MfDwFT-bNVl24FCALRSsMUm1C!-1036170306",
    "Host": "zhuce.nafmii.org.cn",
    "Origin": "http://zhuce.nafmii.org.cn",
    "Referer": "http://zhuce.nafmii.org.cn/fans/publicQuery/manager",
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.132 Safari/537.36",
    "X-Requested-With": "XMLHttpRequest"
}
# 初始化一个空的数据框
temp_df = pd.DataFrame()
# 遍历页面并上传参数来获取数据
for i in range(1, 719):
    payload = {
        "regFileName": "",
        "itemType": "",
        "startTime": "",
        "endTime": "",
        "entityName": "",
        "leadManager": "",
        "regPrdtType": "",
        "page": i,
        "rows": 20
    }
    r = requests.post(obj_url, data=payload, headers=headers)
    if r.status_code == 200:  # 状态码为200就表示获取了数据
        data_json = r.json()  # 数据类型为 json 格式
        for item in data_json["rows"]:  # 遍历 json 的具体格式
            # 将 json 格式转化为数据库
            temp_df = temp_df.append(pd.DataFrame.from_dict(item, orient='index').T, sort=False)
temp_df.reset_index(inplace=True, drop=True)  # 重新设置索引
temp_df.to_csv(Path('你的路径') / "bond_data.csv")
```