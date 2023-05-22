---
description: 成功載入MediaResource後，瀏覽器TVSDK會建立MediaPlayerItem類的實例，以提供對該資源的訪問。
title: 關於MediaPlayerItem類
exl-id: 6e47914c-3d46-4aaf-9144-1a00d886e5bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 關於MediaPlayerItem類{#about-the-mediaplayeritem-class}

成功載入MediaResource後，瀏覽器TVSDK會建立MediaPlayerItem類的實例，以提供對該資源的訪問。

的 `MediaResource` 表示應用程式層向 `MediaPlayer` 載入內容的實例。

的 `MediaPlayer` 解析媒體資源，載入關聯的清單檔案，並解析清單。 這是資源載入進程的非同步部分。 的 `MediaPlayerItem` 實例是在資源解析後生成的，此實例是 `MediaResource`。 瀏覽器TVSDK提供對新建立的 `MediaPlayerItem` 實例 `MediaPlayer.CurrentItem`。

>[!TIP]
>
>必須等待資源成功載入後才能訪問媒體播放器項目。
