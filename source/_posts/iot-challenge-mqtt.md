---
title: IoT 開發小記 - MQTT 交握設計
date: 2023-10-31 10:52:14
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

### Why MQTT?

在 MQTT 上開發相對 WebSocket 來的快速、容易、方便，但相對的缺乏安全性的基礎建設維護安全。
對於 IoT 裝置而言，所需控制裝置數量多，採用 MQTT 似乎是個不錯的選擇，Channel 的廣播設計以及訊息之間的傳遞，讓 Server 端接收訊息的負荷不會過重。

### 幾個設計交握機制上的小 Trick


1. 實現 Zero Touch Enrollment，<br>大型案場所需面對的量級都非常恐怖，於是 Zero Touch 就成了標準配備了：
    + 機器前來報到
    + 伺服器接受訊息，寫入資料後交握加密香料 (Spice)
    + 機器取得香料
    + 機器後須皆用香料加密 Payload
2. Act and Responce，是否伺服器要求的每個動作是否需要回報？
3. Device v.s. Group，怎麼切出這個機制來精準動作，（channel 可以使用 wildcard 聆聽，一大福音！）

先簡單紀錄幾個東西下來，希望接下來可以好好撐過這一年XD