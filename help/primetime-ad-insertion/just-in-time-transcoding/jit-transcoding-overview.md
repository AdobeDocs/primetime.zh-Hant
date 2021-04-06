---
title: 即時轉碼
description: 即時轉碼
copied-description: true
exl-id: 9577e1d5-1462-49d6-9d24-94e74dc9c019
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 即時轉碼{#just-in-time-transcoding}

PrimetimeAd Insertion的功能是即時轉碼和封裝，以確保不相容的廣告創意可在內容串流中正確播放。 它也可以將ID3封包插入廣告片段，以便用於用戶端廣告追蹤。
典型的工作流程如下：

1. Adobe PrimetimeAd Insertion會從客戶的廣告伺服器擷取廣告／創意素材。

1. 如果廣告的創意格式與內容串流在本機上相容，則會將創意插入資訊清單中。

1. 如果廣告的創意格式本身不相容（例如。mp4、.mov、.webm）,PrimetimeAd Insertion會從指定的CDN搜尋預先轉碼的廣告版本。 如果找到廣告，則會插入廣告；否則，廣告會排入轉碼佇列。

1. 轉碼廣告創意素材後，PrimetimeAd Insertion會將該廣告資產的所有後續請求接合至清單中。

PrimetimeAd Insertion支援轉碼大部分視訊和線性格式。 廣告創意轉碼通常在三分鐘內完成。 如需詳細資訊，請連絡您的Primetime支援代表。
