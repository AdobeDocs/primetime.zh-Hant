---
description: MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。
seo-description: MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。
seo-title: 關於MediaPlayerItem類
title: 關於MediaPlayerItem類
uuid: d7f65edf-4693-4b1e-bae0-46fadce98751
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 關於MediaPlayerItem類{#about-the-mediaplayeritem-class}

MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。

媒體資源成功載入後，TVSDK會建立類別的例項， `MediaPlayerItem` 以提供該資源的存取權。

該 `MediaResource` 表示應用層向實例發出的載入內容的 `MediaPlayer` 請求。

解 `MediaPlayer` 析媒體資源、載入相關資訊清單檔案，並解析資訊清單。 這是資源載入過程的非同步部分。 實 `MediaPlayerItem` 例是在資源解析後生成的，此實例是的已解析版本 `MediaResource`。 TVSDK可讓您透過 `MediaPlayerItem``MediaPlayer.CurrentItem`

>[!TIP]
>
>您必須等待資源成功載入，才能存取媒體播放器項目。

