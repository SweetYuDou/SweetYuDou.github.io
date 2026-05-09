---
title: 在Windows上用Claude desktop配置DeepSeek-v4
date: 2026-05-09 15:21:46
tags:
  - ai工具
categories: 学习笔记
---
最近在cc里配deepseek v4挺火的，看了一万个配置教学，我来写个在Windows上的配置教学文档。
### 1. 配置deepseek api
顶部找到Help→Troubleshooting→Enable Developer Mode，点击后同一位置菜单栏会多一个Developer菜单，点击Developer→Configure Third-Party Inference
![](https://a1.boltp.com/2026/05/09/69ff3add1200d.png)
打开后选择Gateway，base URL就填写https://api.deepseek.com/anthropic即可，api填写你自己的deepseek api。往下拉，model list这里要填写claude-deepseek-v4-flash和claude-deepseek-v4-pro，因为现在Claude desktop好像只让用Claude自家的模型了，只不过它是根据模型名称的前缀来识别的，所以这样命名才可以。记得把1M上下文打开。
![](https://a1.boltp.com/2026/05/09/69ff3add17207.png)
配置完点击Apply locally，重启之后正常就能使用了。
### 2. 配置访问网站的白名单
Claude Desktop默认只会访问白名单的网站，正常你无法让模型访问GitHub。在Developer→Configure Third-Party Inference→sandbox&workspace这里，Allowed egress hosts点击Allow all即可。

---
做完上面这些基本就够用了，但是deepseek是纯文本的大模型，如果有代码截图让deepseek分析这种需求的话，可以下载一个合适的MCP来调用免费视觉模型辅助使用。
