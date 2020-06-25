---
title: How to get websocket data from jinshi
date: 2020-06-25 16:09:52
tags: [WebSocket]
categories: [Scarpy]
---

# 金十数据 Websocket 接口

## 目标地址

[金十数据中心-行情中心](https://datacenter.jin10.com/price_wall)

## 接口描述

该接口为 websocket 接口，主要用于获取：股市、外汇、商品、工行、农行的行情数据

## 过程分析

![pic_1](https://jfds-1252952517.cos.ap-chengdu.myqcloud.com/akshare/websocket_1/pic_1.png)

上图中有个 sid 是需要分析获取的

![pic_2](https://jfds-1252952517.cos.ap-chengdu.myqcloud.com/akshare/websocket_1/pic_2.png)

分析出可以通过上述地址来获取 sid，但是随着而来的问题是其中的 t 表面上应该是时间，但是却是字符串的形式，应该是加密导致的。

那么就需要分析 t 是怎么生成的，因为发现 t=NB 经常出现，所以

![pic_3](https://jfds-1252952517.cos.ap-chengdu.myqcloud.com/akshare/websocket_1/pic_3.png)

发现其中的 this.uri，那么就搜 uri 这个参数

![pic_4](https://jfds-1252952517.cos.ap-chengdu.myqcloud.com/akshare/websocket_1/pic_4.png)

把 c() 在 console 中运行，发现是相关的参数，则查找 c 的生成方法

![pic_5](https://jfds-1252952517.cos.ap-chengdu.myqcloud.com/akshare/websocket_1/pic_5.png)

然后查找 r，发现

![pic_6](https://jfds-1252952517.cos.ap-chengdu.myqcloud.com/akshare/websocket_1/pic_6.png)

找出 s 后，利用 execjs 来执行本段代码，可以模拟出 t 这个参数值。

![pic_7](https://jfds-1252952517.cos.ap-chengdu.myqcloud.com/akshare/websocket_1/pic_7.png)

用 session = requests.Session() 来获取对话 session，再依次访问上述的连接。其中

![pic_8](https://jfds-1252952517.cos.ap-chengdu.myqcloud.com/akshare/websocket_1/pic_8.png)

中的 Request Payload 直接使用字符串 post 上去就可以了，注意不用有空格，返回 ok 就成功。

最后连接用 websocket 来访问就好了，下面附上源代码：

```python
import json
import time
from threading import Timer, Event, Thread

import requests
import websocket
import execjs


quotes_js = """
t = +new Date
function n(t) {
                    var e = "";
                    var a = 64;
                    var s = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z", "a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z", "-", "_"];
                    do {
                        e = s[t % a] + e,
                        t = Math.floor(t / a)
                    } while (t > 0);return e
                }
function j() {return n(t)}
"""

js_code = execjs.compile(quotes_js)
js_code.call("j", "")  # 执行js解密代码


def _get_sid() -> str:
    """
    XHR 监听 sid
    需要动态获取sid, 拼接后访问
    https://www.jb51.net/article/149738.htm
    用轮询获取 sid 用 sid 请求
    :return: sid 内容
    :rtype: str
    """
    session = requests.Session()
    url = "https://dc-quote-old.jin10.com/socket.io/"
    params = {
        "EIO": "3",
        "transport": "polling",
        "t": js_code.call("j", ""),
    }
    headers = {
        "accept": "*/*",
        "accept-encoding": "gzip, deflate, br",
        "accept-language": "zh-CN,zh;q=0.9,en;q=0.8",
        "cache-control": "no-cache",
        "origin": "https://datacenter.jin10.com",
        "pragma": "no-cache",
        "referer": "https://datacenter.jin10.com/price_wall",
        "sec-fetch-dest": "empty",
        "sec-fetch-mode": "cors",
        "sec-fetch-site": "same-site",
        "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36",
    }
    r = session.get(url, params=params, headers=headers)
    data_text = r.text
    data_json = json.loads(data_text[data_text.find("{"):])

    url = "https://dc-quote-old.jin10.com/socket.io/"
    params = {
        "EIO": "3",
        "transport": "polling",
        "t": js_code.call("j", ""),
        "sid": data_json["sid"],
    }
    session.get(url, params=params)

    url = "https://dc-quote-old.jin10.com/socket.io/"
    params = {
        "EIO": "3",
        "transport": "polling",
        "t": js_code.call("j", ""),
        "sid": data_json["sid"],
    }
    headers = {
        "content-type": "text/plain;charset=UTF-8",
    }
    data = """1203:42["setAdvSubscription",{"list":["SH1A0001","SZ399001","SH000300","SZ399006","DJI","SPX","GSPTSE","BVSP","MXX","GDAXI","FTSE","FCHI","AEX","IBEX","FTMIB","SSMI","MCX","IRTS","XU100","TA25","TASI","N225","AXJO","HSI","TWII","KS11","JKSE","NSEI","BSESN","DXY","AUDJPY","AUDNZD","AUDUSD","EURAUD","EURCAD","EURCHF","EURGBP","EURJPY","EURNZD","EURUSD","GBPCHF","GBPJPY","GBPUSD","NZDJPY","NZDUSD","USDCAD","USDCHF","USDHKD","USDJPY","AUDCAD","AUDCHF","CADCHF","CADJPY","CHFJPY","EURNOK","EURSEK","EURTRY","GBPAUD","GBPCAD","GBPNZD","NZDCAD","NZDCHF","TRYJPY","USDCNH","USDMXN","USDNOK","USDSEK","USDTRY","USDZAR","ZARJPY","XAUUSD","XAGUSD","USOIL","UKOIL","COPPER","NGAS","BUND","AUTD","AGTD","XPTUSD","XPDUSD","ICNYXAU","ICNYXAG","ICNYXPT","ICNYXPD","IUSDXAU","IUSDXAG","IUSDXPT","IUSDXPD","ICNYWTI","ICNYBRENT","IUSDWTI","IUSDBRENT","ICNYGAS","IUSDGAS","IUSDBRENT1703","ICNYBRENT1703","IUSDWTI1703","ICNYWTI1703","ICNYSOYBEAN1703","IUSDSOYBEAN1703","IUSDCOPPER1703","ICNYCOPPER1703","IEUR","IGBP","IAUD","ICAD","ICHF","IJPY","INZD","ISGD","INOK","ISEK","IGBPUSD","IUSDHKD","IUSDCHF","IUSDSGD","IUSDSEK","IUSDNOK","IUSDJPY","IUSDCAD","IAUDUSD","IEURUSD","INZDUSD","ACNYXAU","ACNYXAG","AUSDXAU","AUSDXAG"]}]"""
    # data = """1203:42["setAdvSubscription",{"list":["SH1A0001","SZ399001","SH000300","SZ399006"]}]"""
    session.post(url, params=params, data=data, headers=headers)

    url = "https://dc-quote-old.jin10.com/socket.io/"
    params = {
        "EIO": "3",
        "transport": "polling",
        "t": js_code.call("j", ""),
        "sid": data_json["sid"],
    }
    session.get(url, params=params)

    url = "https://dc-quote-old.jin10.com/socket.io/"
    params = {
        "EIO": "3",
        "transport": "polling",
        "t": js_code.call("j", ""),
        "sid": data_json["sid"],
    }
    session.get(url, params=params)

    return data_json["sid"]


class HeartbeatThread(Thread):
    """
    心跳
    """
    def __init__(self, event, ws):
        super(HeartbeatThread, self).__init__()
        self.event = event
        self.ws = ws

    def run(self):
        while True:
            # 发送ping包
            self.ws.send("2")
            self.event.wait(timeout=2)


def on_message(ws, message):
    """
    接收信息, 如果要存数据需要在这里处理
    :param ws:
    :type ws:
    :param message:
    :type message:
    :return:
    :rtype:
    """
    print(message)


def on_error(ws, error):
    """

    :param ws:
    :type ws:
    :param error:
    :type error:
    :return:
    :rtype:
    """
    print(error)


def on_close(ws):
    """
    :param ws:
    :type ws:
    :return:
    :rtype:
    """
    print("### closed ###")


def on_open(ws):
    """
    请求连接
    :param ws:
    :type ws:
    :return:
    :rtype:
    """
    ws.send("2probe")
    time.sleep(0.5)  # 发送第二次需要短暂暂停
    ws.send("5")  # 发送字符串 5 来完成握手


def on_emit(ws):
    """
    创建心跳线程
    :param ws: object
    :type ws: websocket object
    :return: None
    :rtype: None
    """
    event = Event()
    heartbeat = HeartbeatThread(event, ws)
    heartbeat.start()


def watch_jinshi():

    websocket.enableTrace(False)
    ws = websocket.WebSocketApp(
        f"wss://dc-quote-old.jin10.com/socket.io/?EIO=3&transport=websocket&sid={_get_sid()}",
        on_message=on_message,
        on_error=on_error,
        on_close=on_close
    )
    ws.on_open = on_open
    t = Timer(20, on_emit, args=(ws,))
    t.start()
    ws.run_forever()


if __name__ == "__main__":
    watch_jinshi()
```
