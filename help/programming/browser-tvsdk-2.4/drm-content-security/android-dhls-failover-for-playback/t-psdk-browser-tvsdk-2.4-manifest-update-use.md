---
description: 您可以開啟此功能並檢查相關事件。
seo-description: 您可以開啟此功能並檢查相關事件。
seo-title: 使用即時主資訊清單更新
title: 使用即時主資訊清單更新
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 使用即時主資訊清單更新{#use-live-master-manifest-update}

您可以開啟此功能並檢查相關事件。

1. 若要開啟即時主資訊清單更新，請設定`NetworkConfiguration.masterUpdateInterval`屬性，以設定更新頻率（以分鐘為單位）。
1. （可選）監聽`MediaPlayerItemEvent.MASTER_UPDATED`事件以追蹤成功的資訊清單更新。
