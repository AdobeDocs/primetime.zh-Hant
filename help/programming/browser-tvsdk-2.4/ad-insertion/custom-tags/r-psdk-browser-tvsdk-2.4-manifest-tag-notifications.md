---
description: MediaPlayerItem.timedMetadata屬性提供對從播放清單/清單標籤或媒體流中的ID3標籤建立的所有TimedMetadata對象的訪問。
title: 清單標籤的通知
exl-id: a8a3cada-d796-460a-bd8f-fc4a2703e7f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 清單標籤的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata屬性提供對從播放清單/清單標籤或媒體流中的ID3標籤建立的所有TimedMetadata對象的訪問。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

的 `MediaPlayerItem.hasTimedMetadata` 屬性指示當前媒體中是否存在訂閱的自定義標籤。 您可以通過偵聽 `Events.TimedMetadataEvent`,MediaPlayer實例在每次新 `TimedMetadata` 對象。
