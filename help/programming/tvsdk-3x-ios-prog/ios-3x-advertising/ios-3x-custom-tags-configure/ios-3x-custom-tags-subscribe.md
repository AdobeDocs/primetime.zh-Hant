---
description: TVSDK會在每次訂閱的標籤物件出現在內容資訊清單中時，為這些物件準備好PTTimedMetadata物件。
title: 訂閱自訂標籤
exl-id: 5074e622-8824-4253-a668-485e2f68f156
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 訂閱自訂標籤 {#subscribe-to-custom-tags}

TVSDK會在每次訂閱的標籤物件出現在內容資訊清單中時，為這些物件準備好PTTimedMetadata物件。

在播放開始之前，您必須訂閱標籤。
若要接收有關HLS資訊清單中自訂標籤的通知：

1. 將包含自訂標籤的陣列傳遞至，以全域設定自訂廣告標簽名稱 `setSubscribedTags` 在 `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >您必須包含 `#` 使用HLS資料流時的首碼。

   例如：

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
