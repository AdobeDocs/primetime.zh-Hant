---
description: MediaResource代表即將由MediaPlayer例項載入的內容。
title: MediaPlayer和MediaResource類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# MediaPlayer和MediaResource類別 {#mediaplayer-and-mediaresource-classes}

MediaResource代表即將由MediaPlayer例項載入的內容。

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

TVSDK提供了透過使用載入及準備內容以進行播放的方法。 `replaceCurrentResource` 中的方法 `MediaPlayer`. 此方法會採用兩個引數，一個例項 `MediaPlayerResource` 以及（選擇性）的例項 `MediaPlayerItemConfig`，可用來傳遞應用程式定義的自訂引數。

* 如需詳細資訊，請參閱mediaplayer-reuse-or-remove 。
* 詳細資訊： `MediaPlayerResource`，請參閱media-resource-create
