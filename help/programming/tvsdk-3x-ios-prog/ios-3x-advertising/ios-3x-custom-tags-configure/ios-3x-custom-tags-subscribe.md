---
description: 每次在內容清單中遇到這些對象時，TVSDK都會為訂閱的標籤準備PTTimedMetadata對象。
title: 訂閱自定義標籤
exl-id: 5074e622-8824-4253-a668-485e2f68f156
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 訂閱自定義標籤 {#subscribe-to-custom-tags}

每次在內容清單中遇到這些對象時，TVSDK都會為訂閱的標籤準備PTTimedMetadata對象。

在播放開始之前，您必須訂閱標籤。
要通知有關HLS清單中的自定義標籤：

1. 通過將包含自定義標籤的陣列傳遞到 `setSubscribedTags` 在 `PTSDKConfig`。

   >[!IMPORTANT]
   >
   >必須包括 `#` 使用HLS流時的前置詞。

   例如：

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
