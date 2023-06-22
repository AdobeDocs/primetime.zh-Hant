---
description: TVSDK會在每次訂閱標籤物件出現在內容資訊清單中時，為這些物件準備TimedMetadata物件。
title: 訂閱自訂標籤
exl-id: c2b5b78c-5fe7-4564-ab6b-38b3c00fd3d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 訂閱自訂標籤 {#subscribe-to-custom-tags}

TVSDK會在每次訂閱標籤物件出現在內容資訊清單中時，為這些物件準備TimedMetadata物件。

在播放開始之前，您必須訂閱標籤。 若要接收有關HLS資訊清單中自訂標籤的通知：

1. 將包含自訂標籤的陣列傳遞至，以全域設定自訂廣告標簽名稱 `setSubscribedTags` 在 `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >您必須包含 `#` 使用HLS資料流時的首碼。

   例如：

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```
