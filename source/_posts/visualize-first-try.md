---
title: 視覺化探險日記(1) - 以 python-docs-zh-tw 為例
date: 2023-09-11 22:35:00
tags:
- dev
- diary
---

自從加入了 [python-docs-zh-tw](https://github.com/python/python-docs-zh-tw) 翻譯計畫，好像越做越有心得(?)
畢竟以前沒有這種可以加入社群貢獻的機會，所以這次我沒有放掉這個機會了。

本次任務是因為取得了每個頁面的瀏覽次數等資料 [1] ，
我想配合上 Organizer 一直有在使用的 [potodo](https://pypi.org/project/potodo/) 工具去計算出每個 po 檔案的翻譯完成度為何 [2] ，
進行了本次的資料視覺化挑戰。

{% asset_img code_views.png [code_pageviews] %}
> [1] : [python-docs-zh-tw](https://github.com/python/python-docs-zh-tw) 個別頁面的瀏覽資料

{% asset_img code_potodo.png [code_potodo] %}
> [2] : [python-docs-zh-tw](https://github.com/python/python-docs-zh-tw) 各項檔案的翻譯完成度資料

本來想說都靠著前人有經驗產生過的資料，也來自己產生看看，
產生過程都沒問題，**這兩個檔案的正規化 (Normalized) 才是挑戰**。

這個機會又讓我跟 [Pandas.DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) 再次熟悉了一下。 

最後的結果如下：
1. 頁面瀏覽次數及訪客數的曲線圖
  + Color => Folder
  + X-axis => Visitors
  + Y-axis => Pageviews
  + Filter :  500 < Pageviews < 2500 
  + (500 以下過於密集、2500 以上只有Tutorial/index, Library/datetime )
{% asset_img pageviews_visitors.png [pageviews_visitors] %}

2. 頁面瀏覽次數及訪客數的曲線圖
  + Color => Filename
  + X-axis => Pageviews
  + Y-axis => Translated Percent
  + Filter : 500 < Pageviews , Remove Tutorial, Installing
  + Note : 移掉後面兩個是不知道為什麼跟 potodo 的資料對不上 
  + Note : 圖片中 Translated Percent 為 0 的也是 potodo 無資料
{% asset_img pageviews_translated.png [pageviews_translated] %}

以前擅長的都是結合 GeoData 的地圖視覺化，這次挑戰純數字資料的視覺化是個挑戰啊。

P.S. 好的資料集真的很重要，向所有的 Data Scientist 看齊！
P.P.S. 不小心喚起了記憶，大學時期分數最慘的科目就是*統計*。