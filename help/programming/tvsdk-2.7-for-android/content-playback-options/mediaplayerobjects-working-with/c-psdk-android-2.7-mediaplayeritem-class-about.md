---
description: 在您成功載入MediaResource物件後，TVSDK會建立MediaPlayerItem類別的例項，以提供該資源的存取權。
seo-description: 在您成功載入MediaResource物件後，TVSDK會建立MediaPlayerItem類別的例項，以提供該資源的存取權。
seo-title: 關於MediaPlayerItem類
title: 關於MediaPlayerItem類
uuid: 2d37f358-d158-481b-81d5-27546e9c2e0e
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# 關於MediaPlayerItem類{#about-the-mediaplayeritem-class}

MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。

在您成功載入MediaResource物件後，TVSDK會建立MediaPlayerItem類別的例項，以提供該資源的存取權。

`MediaResource`代表應用層向`MediaPlayer`實例發出的用於載入內容的請求。

`MediaPlayer`會解析媒體資源、載入相關資訊清單檔案，並解析資訊清單。 這是資源載入過程的非同步部分。 `MediaPlayerItem`實例是在資源解析後生成的，此實例是`MediaResource`的已解析版本。 TVSDK可透過`MediaPlayer.CurrentItem`存取新建立的`MediaPlayerItem`例項。

>[!TIP]
>
>您必須等待資源成功載入，才能存取媒體播放器項目。