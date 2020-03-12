---
description: 每當內容資訊清單中出現這些物件時，TVSDK就會為訂閱的標籤準備PTTimedMetadata物件。
seo-description: 每當內容資訊清單中出現這些物件時，TVSDK就會為訂閱的標籤準備PTTimedMetadata物件。
seo-title: 訂閱自訂標籤
title: 訂閱自訂標籤
uuid: de66d3db-46d1-485f-9d3a-6e28495bfb13
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 訂閱自訂標籤 {#subscribe-to-custom-tags}

每當內容資訊清單中出現這些物件時，TVSDK就會為訂閱的標籤準備PTTimedMetadata物件。

播放開始前，您必須訂閱標籤。
要獲得有關HLS清單中自定義標籤的通知：

1. 將包含自訂標籤的陣列傳遞至中，以全域設定自訂廣告標 `setSubscribedTags` 記名 `PTSDKConfig`稱。

   >[!IMPORTANT]
   >
   >使用HLS流時必 `#` 須包含前置詞。

   例如：

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

