---
description: TVSDK會在每次在內容資訊清單中遇到訂閱的標籤時，準備這些物件的PTTimedMetadata物件。
title: 訂閱自訂標籤
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 訂閱自訂標籤 {#subscribe-to-custom-tags}

TVSDK會在每次在內容資訊清單中遇到訂閱的標籤時，準備這些物件的PTTimedMetadata物件。

在播放開始之前，您必須訂閱標籤。
若要接收有關HLS資訊清單中自訂標籤的通知：

1. 將包含自訂標籤的陣列傳遞至，以全域設定自訂廣告標簽名稱 `setSubscribedTags` 在 `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >您必須包含 `#` 使用HLS資料流時的前置詞。

   例如：

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
