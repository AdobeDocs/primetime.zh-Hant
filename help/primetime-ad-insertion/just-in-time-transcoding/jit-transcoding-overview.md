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

PrimetimeAd Insertion提供即時轉碼和封裝功能，以確保不相容的廣告創意內容可在內容串流中正確播放。 它也可以將ID3封包插入可用於使用者端廣告追蹤的廣告片段中。
典型的工作流程如下：

1. Adobe PrimetimeAd Insertion會從客戶的廣告伺服器擷取廣告/創意。

1. 如果廣告的創意格式與內容串流原生相容，則會將創意插入資訊清單中。

1. 如果廣告的創意格式本身不相容（例如.mp4、.mov、.webm），PrimetimeAd Insertion會從指定的CDN搜尋預先轉碼版本的廣告。 如果找到，則會插入該廣告；否則，會將該廣告排入轉碼佇列。

1. 轉碼廣告創意後，PrimetimeAd Insertion會將該廣告資產的所有後續請求拼接到資訊清單中。

PrimetimeAd Insertion支援大多數視訊和線性格式的轉碼。 廣告創意轉碼通常會在三分鐘內發生。 如需詳細資訊，請聯絡您的Primetime支援代表。
