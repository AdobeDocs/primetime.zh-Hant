---
description: MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。
seo-description: MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。
seo-title: 關於MediaPlayerItem類
title: 關於MediaPlayerItem類
uuid: 531dd1a6-d72c-4ae3-9c3f-2f1d854245c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 關於MediaPlayerItem類{#about-the-mediaplayeritem-class}

MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

媒體資源成功載入後，TVSDK會建立類別的例項， `MediaPlayerItem` 以提供該資源的存取權。

該 `MediaResource` 表示應用層向實例發出的載入內容的 `MediaPlayer` 請求。

解 `MediaPlayer` 析媒體資源、載入相關資訊清單檔案，並解析資訊清單。 這是資源載入過程的非同步部分。 實 `MediaPlayerItem` 例是在資源解析後生成的，此實例是的已解析版本 `MediaResource`。 TVSDK可讓您透過存取新建 `MediaPlayerItem` 的例項 `MediaPlayer.currentItem`。

>[!TIP]
>
>您必須等待資源成功載入，才能存取媒體播放器項目。

