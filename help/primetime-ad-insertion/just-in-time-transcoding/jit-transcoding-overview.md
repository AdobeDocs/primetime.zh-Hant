---
title: 即時轉碼
description: 即時轉碼
copied-description: true
exl-id: 9577e1d5-1462-49d6-9d24-94e74dc9c019
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 即時轉碼 {#just-in-time-transcoding}

黃金時段Ad Insertion提供即時轉碼和打包功能，以確保不相容的廣告創意能夠在內容流中正確回放。 它還可以將ID3資料包注入可用於客戶端和跟蹤的ad片段中。
典型的工作流如下：

1. Adobe PrimetimeAd Insertion從客戶的廣告伺服器中獲取廣告/創意。

1. 如果廣告的創意格式與內容流本機相容，則創意被插入清單中。

1. 如果廣告的創作格式本機上不相容（例如，.mp4、.mov、.webm），則黃金時段Ad Insertion從指定CDN搜索預轉碼版本的廣告。 如果找到一個，則插入廣告；否則，該廣告將排隊等待轉碼。

1. 廣告創意轉碼後，黃金時段Ad Insertion會將該廣告資產的所有後續要求整合至清單。

黃金時段Ad Insertion支援大多數視頻和線性格式的轉碼。 廣告創意轉碼通常在三分鐘內完成。 有關更多詳情，請聯繫您的黃金時段支援代表。
