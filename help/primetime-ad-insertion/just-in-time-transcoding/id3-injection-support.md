---
description: 即時轉碼可以將ID3定時元資料注入廣告創意，以便於客戶端廣告跟蹤。
title: 使用即時轉碼來注入ID3定時元資料標籤
exl-id: 6171223a-71f9-45a2-a3f5-7ede4a9b101a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 使用即時轉碼來注入ID3定時元資料標籤 {#using-crs-to-inject-id-timed-metadata-tags}

CRS可以將ID3定時元資料注入廣告創意，以便於客戶端廣告跟蹤。

客戶端播放器讀取ID3元資料以啟用幀精確和跟蹤。

>[!NOTE]
>
>ID3隻針對Safari/iOS的定時元資料注入函式。

## ID3注入的CRS工作流 {#workflow-for-crs-for-id3-injection}

如果黃金時段Ad Insertion接收 `ptplayer=ios-mobileweb` 參數，在將ID3資料包上傳到相應的ad儲存CDN之前，先將ID3資料包注入轉碼的ad creative。
