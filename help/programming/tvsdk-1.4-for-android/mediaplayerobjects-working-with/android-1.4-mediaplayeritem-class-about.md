---
description: MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。
title: 關於MediaPlayerItem類別
exl-id: 07105fab-0338-4410-93f3-e337d46d9de5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 關於MediaPlayerItem類別{#about-the-mediaplayeritem-class}

MediaPlayer物件代表您的媒體播放器。 MediaPlayerItem代表播放器上的音訊或視訊。

成功載入媒體資源後，TVSDK會建立 `MediaPlayerItem` 類別以提供對該資源的存取權。

此 `MediaResource` 代表應用程式層核發給 `MediaPlayer` 例項以載入內容。

此 `MediaPlayer` 解析媒體資源、載入關聯的資訊清單檔案，以及剖析資訊清單。 這是資源載入程式的非同步部分。 此 `MediaPlayerItem` 執行個體會在資源解析後產生，而且此執行個體是的解析版本 `MediaResource`. TVSDK可讓您存取新建立的 `MediaPlayerItem` 執行個體到 `MediaPlayer.CurrentItem`

>[!TIP]
>
>您必須等待資源成功載入，才能存取媒體播放器專案。
