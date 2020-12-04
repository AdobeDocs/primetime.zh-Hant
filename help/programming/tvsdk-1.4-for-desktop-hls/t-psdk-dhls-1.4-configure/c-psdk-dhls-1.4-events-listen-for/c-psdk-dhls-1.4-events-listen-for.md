---
description: 來自TVSDK的事件會指出播放器的狀態、發生的錯誤、您所要求的動作的完成，例如視訊開始播放，或是隱式發生的動作，例如廣告完成。
seo-description: 來自TVSDK的事件會指出播放器的狀態、發生的錯誤、您所要求的動作的完成，例如視訊開始播放，或是隱式發生的動作，例如廣告完成。
seo-title: 監聽Primetime Player活動
title: 監聽Primetime Player活動
uuid: e72782bf-9d26-4285-85e4-fd4d803c1bbe
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# 概述{#listen-for-primetime-player-events-overview}

來自TVSDK的事件會指出播放器的狀態、發生的錯誤、您所要求的動作的完成，例如視訊開始播放，或是隱式發生的動作，例如廣告完成。

由於您的應用程式需要回應其中許多事件，因此您必須實作事件處理常式，並向TVSDK註冊這些常式。 這些常式會呼叫相關的TVSDK方法以適當回應。

以下是有關事件的其他資訊：

* 視訊播放的即時性要求許多TVSDK作業需要非同步（非封鎖）活動。
* TVSDK支援事件導向視訊播放器。

   它提供與播放程式中所有重要步驟對應的事件。 您可以使用平台的事件機制註冊這些事件，並建立事件處理常式，以便在這些事件發生時呼叫。 *`Event Handlers`* 也稱為回呼常式或事件偵聽程式。TVSDK提供事件處理常式可使用的完整方法範圍。
* 您的應用程式通常會啟動非封鎖作業，例如要求視訊開始播放。

   TVSDK會透過分派事件（例如視訊何時開始播放，以及視訊結束時的事件）與您的應用程式進行非同步通訊。 其他事件可指出您播放器中的狀態變更和錯誤狀況。 您的事件處理常式會採取適當的動作。

