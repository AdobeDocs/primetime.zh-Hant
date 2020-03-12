---
description: 在您成功載入MediaResource物件後，TVSDK會建立MediaPlayerItem類別的例項，以提供該資源的存取權。
seo-description: 在您成功載入MediaResource物件後，TVSDK會建立MediaPlayerItem類別的例項，以提供該資源的存取權。
seo-title: 關於MediaPlayerItem類
title: 關於MediaPlayerItem類
uuid: 2d37f358-d158-481b-81d5-27546e9c2e0e
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 關於MediaPlayerItem類 {#about-the-mediaplayeritem-class}

MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。

在您成功載入MediaResource物件後，TVSDK會建立MediaPlayerItem類別的例項，以提供該資源的存取權。

該 `MediaResource` 表示應用層向實例發出的載入內容的 `MediaPlayer` 請求。

解 `MediaPlayer` 析媒體資源、載入相關資訊清單檔案，並解析資訊清單。 這是資源載入過程的非同步部分。 實 `MediaPlayerItem` 例是在資源解析後生成的，此實例是的已解析版本 `MediaResource`。 TVSDK可讓您透過存取新建 `MediaPlayerItem` 的例項 `MediaPlayer.CurrentItem`。

>[!TIP]
>
>您必須等待資源成功載入，才能存取媒體播放器項目。