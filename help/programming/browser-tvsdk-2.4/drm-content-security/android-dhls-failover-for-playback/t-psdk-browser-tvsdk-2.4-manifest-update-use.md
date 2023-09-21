---
description: 您可以開啟此功能並檢查相關事件。
title: 使用即時主要資訊清單更新
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# 使用即時主要資訊清單更新{#use-live-master-manifest-update}

您可以開啟此功能並檢查相關事件。

1. 若要開啟即時主要資訊清單更新，請透過設定 `NetworkConfiguration.masterUpdateInterval` 屬性。
1. 選擇性地透過聆聽 `MediaPlayerItemEvent.MASTER_UPDATED` 事件。
