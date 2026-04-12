---
title: unsloth studio微调尝试
date: 2026-04-12 15:18:30
tags: 微调
categories: 学习笔记
---

​	毕设要做大模型微调，由于之前实习的时候有用llama-factory微调的经验，所以本来想直接用llama-factory来单卡微调的。结果在modelscope上下载模型时意外发现了unsloth这个大模型微调工具，和llama-factory一样，开发了gui界面，也就是unsloth studio，而且声称其单卡微调速度更快，内存占用更少，于是我想试一下用unsloth来微调，正好我目前也是在autodl上租单卡服务器。结果折腾了半天还是放弃了😭。写篇文章记录一下，希望不久能重新跑成功。

### 尝试在Windows上跑通

​	我的思路：先在本地把训练跑通，再把文件和环境上传到服务器上正式训练。本地os是Windows10，按照文档步骤在powershell里运行

```cmd
irm https://unsloth.ai/install.ps1 | iex
```

​	结果发现这个脚本只支持创建python自带的虚拟环境venv，不支持conda环境，原因在注释中写道：conda 自带的 CPython 在 Windows 上可能导致 torch 的 c10.dll 加载问题。...也行吧，脚本运行完后，成功launch unsloth。但是似乎不能像llama-factory一样加载当前目录下的模型文件，只能加载.cache/huggingface/hub中的模型。

![](https://www.helloimg.com/i/2026/04/12/69db4c922e007.png)

![](https://www.helloimg.com/i/2026/04/12/69db4c91ebf0f.png)

​	想了想算了，反正只是跑通训练，就暂时不管这个设置好参数start training了。结果训练报错，说无法下载causall-conv1d，是个专为时间序列数据处理优化的库，关键是只适用于Linux...我去不早说？不下载也可以，但是就用不了flash attention2等加速方式，虽然我也没在studio界面上找到可以修改加速方式的地方，最终放弃在Windows上跑通了，转战Linux。

### 尝试在Linux上跑通

​	用Linux启动unsloth studio，然后端口转发到本地，用本地浏览器打开unsloth studio，结果发现数据集上传方式只能从本地拖动上去（？）上传上去后view dataset一直加载不出来...然后start training在Installing causal-conv1d from PyPI这一步卡住了，还是在给服务器配置代理的条件下，等了20min无反应，没办法租服务器太贵了，我不想等了就直接投靠回llama-factory了

![](https://www.helloimg.com/i/2026/04/12/69db51c564d34.png)

### 总结

​	还没试过用unsloth core来开发，只是我比较习惯gui界面。写篇文章记录一下踩过的坑，我还是很希望能够用unsloth core或者unsloth studio跑一次单卡训练的👉👈
