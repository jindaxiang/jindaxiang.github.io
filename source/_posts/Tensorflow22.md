---
title: How to install TensorFlow 2.2 on Windows 10
date: 2020-05-13 16:09:52
tags: [TensorFlow]
categories: [Python]
---

# How to install TensorFlow 2.2 on Windows 10
>TensorFlow 2.2 is the latest version for now


```powershell
conda create -n tf_test python  # 安装最新版 Python
conda activate tf_test  # 进入所创建的 tf_test 这个虚拟环境
pip install tensorflow  # 安装适配当前虚拟环境 Python 版本的 TensorFlow
pip install cudnn # 自动安装最新的 TensorFlow 配套支持库
```

1. If return **grpcio** error, please `pip install grpcio` via proxy
2. If return can not find DLL error, please `conda install cudnn`