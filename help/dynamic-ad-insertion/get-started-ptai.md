---
title: 開始使用Adobe Primetime廣告插入
description: Adobe Primetime廣告插入快速入門
translation-type: tm+mt
source-git-commit: 2a9bb089cda2b315f91b30d5cab0db9b3e372799
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# 開始使用Adobe Primetime廣告插入{#ptai-get-started}

Primetime廣告插入可協調提供內容和廣告的系統，以建立個人化的串流廣告體驗，然後追蹤廣告商的廣告播放。

Primetime廣告插入透過重新編寫視訊清單與視訊傳送用戶端應用程式互動，為每個檢視者提供目標廣告和個人化體驗。這些清單結合了從廣告伺服器傳送的內容和廣告，並可選擇包含詳細廣告追蹤指示的中繼資料。 Primetime廣告插入支援用戶端和伺服器端廣告追蹤。

在正確設定系統後，典型的工作流程可能如下所示：

1. 用戶端應用程式會產生包含視訊串流資訊的[引導URL](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)，並傳送GET要求至Primetime廣告插入。

1. Primetime廣告插入會從發行者的CDN將內容資訊清單傳回用戶端應用程式，以回應。

1. 用戶端應用程式會在產生的資訊清單中選擇適當的串流以播放並要求插入Primetime廣告。

1. Primetime廣告插入從內容CDN擷取所要求的串流、剖析／讀取任何提示資訊、對廣告伺服器進行呼叫並視需要取代廣告插播。

1. Primetime廣告插入可重寫資源URL並偵測廣告創意是否需要轉碼，以標準化資訊清單。<!-- see [Just-in-time ad transcoding](just-in-time-transcoding.md) and [packaging](just-in-time-repackaging.md).-->

1. Primetime廣告插入會擷取所需廣告創作元素，並將適當片段插入資訊清單。

1. Primetime廣告插入將最終的銜接清單（包括廣告）傳送至用戶端應用程式以供播放。

1. 您可以透過用戶端或伺服器端廣告追蹤來測量廣告傳遞和可見性，請參閱[設定廣告追蹤](set-up-ad-tracking.md)。

Primetime廣告插入支援HLS/DASH的大多數客戶機配置。
