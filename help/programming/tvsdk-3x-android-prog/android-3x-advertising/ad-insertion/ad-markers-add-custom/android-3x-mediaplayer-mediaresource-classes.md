---
description: MediaResource代表即將由MediaPlayer例項載入的內容。
title: MediaPlayer和MediaResource類別
exl-id: 5321a9b5-bdc2-4287-85a6-4571e93c7f14
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# MediaPlayer和MediaResource類別 {#mediaplayer-and-mediaresource-classes}

MediaResource代表即將由MediaPlayer例項載入的內容。

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

TVSDK提供載入及準備內容以供播放的方法，方法是使用 `replaceCurrentResource` 中的方法 `MediaPlayer`. 此方法會採用兩個引數，一個例項 `MediaPlayerResource` 以及（選擇性）的執行個體 `MediaPlayerItemConfig`，可用來傳遞應用程式定義的自訂引數。

* 如需詳細資訊，請參閱 [重複使用或移除MediaPlayer執行個體](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayerobjects-working-with/android-3x-mediaplayer-reuse-or-remove.md).
* 詳細資訊： `MediaPlayerResource`，請參閱 [建立媒體資源](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-create.md).
