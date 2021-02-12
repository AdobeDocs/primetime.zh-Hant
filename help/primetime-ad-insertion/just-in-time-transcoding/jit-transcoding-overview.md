---
title: 即時轉碼
description: null
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# 即時轉碼{#just-in-time-transcoding}

Primetime廣告插入功能可即時轉碼和封裝，以確保不相容的廣告創意素材可在內容串流中正確播放。 它也可以將ID3封包插入廣告片段，以便用於用戶端廣告追蹤。
典型的工作流程如下：

1. Adobe Primetime廣告插入會從客戶的廣告伺服器擷取廣告／創意素材。

1. 如果廣告的創意格式與內容串流在本機上相容，則會將創意插入資訊清單中。

1. 如果廣告的創意格式本身不相容（例如。mp4、.mov、.webm）,Primetime廣告插入會從指定的CDN搜尋預先轉碼的廣告版本。 如果找到廣告，則會插入廣告；否則，廣告會排入轉碼佇列。

1. 轉碼廣告創意素材後，Primetime廣告插入會將該廣告資產的所有後續請求接合到清單中。

Primetime廣告插入支援轉碼大部分視訊和線性格式。 廣告創意轉碼通常在三分鐘內完成。 如需詳細資訊，請連絡您的Primetime支援代表。
