---
description: MediaPlayerItem.timedMetadata屬性可讓您存取所有TimedMetadata物件，這些物件是從播放清單/資訊清單標籤或媒體串流中的ID3標籤建立的。
title: 資訊清單標籤的通知
exl-id: a8a3cada-d796-460a-bd8f-fc4a2703e7f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 資訊清單標籤的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata屬性可讓您存取所有TimedMetadata物件，這些物件是從播放清單/資訊清單標籤或媒體串流中的ID3標籤建立的。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

此 `MediaPlayerItem.hasTimedMetadata` 屬性指出目前媒體中是否存在訂閱的自訂標籤。 您可以監聽以下專案來監視定時中繼資料： `Events.TimedMetadataEvent`，MediaPlayer例項每次傳送新訊息時 `TimedMetadata` 物件已建立。
