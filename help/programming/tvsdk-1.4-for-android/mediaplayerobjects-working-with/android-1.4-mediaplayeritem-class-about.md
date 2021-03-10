---
description: MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。
title: 關於MediaPlayerItem類
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 關於MediaPlayerItem類{#about-the-mediaplayeritem-class}

MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。

媒體資源成功載入後，TVSDK會建立`MediaPlayerItem`類別的例項，以提供該資源的存取權。

`MediaResource`代表應用層向`MediaPlayer`實例發出的用於載入內容的請求。

`MediaPlayer`會解析媒體資源、載入相關資訊清單檔案，並解析資訊清單。 這是資源載入過程的非同步部分。 `MediaPlayerItem`實例是在資源解析後生成的，此實例是`MediaResource`的已解析版本。 TVSDK可透過`MediaPlayer.CurrentItem`存取新建立的`MediaPlayerItem`例項

>[!TIP]
>
>您必須等待資源成功載入，才能存取媒體播放器項目。

