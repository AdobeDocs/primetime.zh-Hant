---
description: 每當內容資訊清單中出現這些物件時，TVSDK就會為訂閱的標籤準備PTTimedMetadata物件。
title: 訂閱自訂標籤
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# 訂閱自訂標籤{#subscribe-to-custom-tags}

每當內容資訊清單中出現這些物件時，TVSDK就會為訂閱的標籤準備PTTimedMetadata物件。

播放開始前，您必須訂閱標籤。
要獲得有關HLS清單中自定義標籤的通知：

1. 將包含自訂標籤的陣列傳遞至`PTSDKConfig`中的`setSubscribedTags`，以全域設定自訂廣告標籤名稱。

   >[!IMPORTANT]
   >
   >使用HLS流時必須包含`#`前置詞。

   例如：

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

