---
description: 成功載入MediaResource後，瀏覽器TVSDK會建立MediaPlayerItem類別的執行個體，以提供對該資源的存取權。
title: 關於MediaPlayerItem類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 關於MediaPlayerItem類別{#about-the-mediaplayeritem-class}

成功載入MediaResource後，瀏覽器TVSDK會建立MediaPlayerItem類別的執行個體，以提供對該資源的存取權。

此 `MediaResource` 代表應用程式層核發給 `MediaPlayer` 例項以載入內容。

此 `MediaPlayer` 解析媒體資源、載入關聯的資訊清單檔案，並剖析資訊清單。 這是資源載入程式的非同步部分。 此 `MediaPlayerItem` 執行個體會在資源解析後產生，此執行個體是的解析版本 `MediaResource`. 瀏覽器TVSDK提供新建立的存取權 `MediaPlayerItem` 執行個體至 `MediaPlayer.CurrentItem`.

>[!TIP]
>
>您必須先等候資源成功載入，才能存取媒體播放器專案。
