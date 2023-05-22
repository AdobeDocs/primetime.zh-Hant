---
description: MediaPlayer對象表示您的媒體播放器。 MediaPlayerItem表示播放器上的音頻或視頻。
title: 關於MediaPlayerItem類
exl-id: ff7011ae-57d7-41e1-98be-5319bdc6f799
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 關於MediaPlayerItem類{#about-the-mediaplayeritem-class}

MediaPlayer對象表示您的媒體播放器。 MediaPlayerItem表示播放器上的音頻或視頻。

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

成功載入媒體資源後，TVSDK將建立 `MediaPlayerItem` 類以提供對該資源的訪問。

的 `MediaResource` 表示應用程式層向 `MediaPlayer` 載入內容的實例。

的 `MediaPlayer` 解析媒體資源，載入關聯的清單檔案，並解析清單。 這是資源載入進程的非同步部分。 的 `MediaPlayerItem` 實例是在資源解析後生成的，此實例是 `MediaResource`。 TVSDK提供對新建立的 `MediaPlayerItem` 實例 `MediaPlayer.currentItem`。

>[!TIP]
>
>必須等待資源成功載入後才能訪問媒體播放器項目。
