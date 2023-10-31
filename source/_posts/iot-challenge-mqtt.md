---
title: iot-challenge-mqtt
date: 2023-09-12 10:52:14
tags:
- dev
- mqtt
---

前陣子公司開了一個新案子，目的是要跟 IoT 裝置對接，
身為一個 FullStack Web Developer，聽到的當下眉頭不自覺的緊縮了了一下。

我們需要自行設計、架設裝置以及伺服器之間，兩兩互相交握的機制。
(下一個目標可不可以往 System Architect 前進呢？)

原本沒有那害怕的原因是因為公司有在某個 Cloud Platform 上實做一個 IoT Edge Server，
然而這個案子希望可以在任何機器上都可以部屬，那我看就是用 Docker Container 來處理了。

### MQTT 運作原理
