---
title: KKTIX Banner Generator (活動旗幟產生器)
date: 2023-10-01 11:29:33
tags:
- dev
- marketing
---

在[上次文章](https://hi.rockleon.dev/blog/2023/09/11/visualize-first-try/)中有提到加入了 pydoc 翻譯計畫，在 2023 / 10月舉辦一個實體活動，本次是第一次實際餐與籌備，所以意外的接觸到了 KKTIX 後台。

[python-docs-zh-tw](https://github.com/python/python-docs-zh-tw) 翻譯計畫是 [sciwork](https://sciwork.dev/) 社群所支持的專案之一，很多所需的資源都是仰賴 sciwork 的基礎建設而成的，包含這次的售票系統的 KKTIX 也由他們提供。

在 KKTIX 的後台中，提供了活動圖片的上傳空間，同時間他也會代表 html meta tag 的圖片，同時意味著，如果在社群媒體平台分享的話，可以有個小縮圖可以看到圖片是甚麼。

在社群沒有平面設計師協助的情況之下，小弟我自告奮勇地寫了一個 Banner Generator：

{% asset_img banner-pydoc.png [banner-pydoc] %}
> [python-docs-zh-tw](https://github.com/python/python-docs-zh-tw) 2023/10 sprint

Generator 的腳本中，我使用了以下的 techstack (當然是 developed with Python):
1. [Pillow](https://pillow.readthedocs.io/en/stable/): 圖片編輯
2. [Unsplash API](https://unsplash.com/documentation): 隨機圖片的提供者

其中遇到的幾個有趣小東西值得紀錄一下：
1. Unsplash API 取得相片 URL 後，Requests GET 所得到的會直接是 Bytes 而不是 String，原本挖 Stack Overflow 的時候，有看到一個 Reference 指出需要用 StringIO 實作解析圖片， **我被誤導了** ，明明看過相片 URL 本身一定會回傳 Bytes，為甚麼還要用 StringIO 去解析呢？？ **(暈頭轉向的我)**
2. 如果是合成透明圖片 (圖層) 的話，一定要用上 ```Image.alpha_composite()```，不然你的圖片會有很精美的方格子出現，也就是大家最喜歡的 png 透明圖層具現化(?)

{% asset_img code_bytesio.png [code_bytesio] %}
> Using PIL.Image to open ByteIO Binary Image

{% asset_img code_alphalayer.png [code_alphalayer] %}
> Image.alpha_composite() to composite the image 

以上就是這次的開發小記，總計 2 個小時研究及將 PoC 開發完畢，甚是感動。

Github Repo : https://github.com/sciwork/banner_generator
