---
description: 您可以開啟此功能並檢查相關事件。
title: 使用即時主資訊清單更新
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---


# 使用即時主資訊清單更新{#use-live-master-manifest-update}

您可以開啟此功能並檢查相關事件。

1. 若要開啟即時主資訊清單更新，請設定`NetworkConfiguration.masterUpdateInterval`屬性，以設定更新頻率（以分鐘為單位）。
1. （可選）監聽`MediaPlayerItemEvent.MASTER_UPDATED`事件以追蹤成功的資訊清單更新。
