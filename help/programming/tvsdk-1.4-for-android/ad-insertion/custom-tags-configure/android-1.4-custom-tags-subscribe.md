---
description: 每次在內容資訊清單中遇到這些物件時，TVSDK會為訂閱的標籤準備TimedMetadata物件。
seo-description: 每次在內容資訊清單中遇到這些物件時，TVSDK會為訂閱的標籤準備TimedMetadata物件。
seo-title: 訂閱自訂標籤
title: 訂閱自訂標籤
uuid: fe8ba34d-66fc-43bb-b98e-659c1702d1e0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 1%

---


# 訂閱自訂標籤{#subscribe-to-custom-tags}

每次在內容資訊清單中遇到這些物件時，TVSDK會為訂閱的標籤準備TimedMetadata物件。

播放開始前，您必須訂閱標籤。
要獲得有關HLS清單中自定義標籤的通知：

將包含自訂標籤的陣列傳遞至`MediaPlayerItemConfig`中的`setSubscribedTags`，以全域設定自訂廣告標籤名稱。

>[!IMPORTANT]
>
>使用HLS流時必須包含`#`前置詞。

例如：

```java
String[] array = new String[3]; 
array[0] = "#EXT-X-ASSET"; 
array[1] = "#EXT-X-BLACKOUT"; 
array[2] = "#EXT-OATCLS-SCTE35"; 
MediaPlayerItemConfig.setSubscribedTags(array);
```

