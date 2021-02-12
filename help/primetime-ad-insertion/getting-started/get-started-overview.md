---
title: 開始使用Adobe Primetime廣告插入
description: Adobe Primetime廣告插入快速入門
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# 開始使用Adobe Primetime廣告插入{#ptai-get-started}

Primetime廣告插入可協調提供內容和廣告的系統，以建立個人化的串流廣告體驗，然後追蹤廣告商的廣告播放。

Primetime廣告插入可透過重新編寫視訊清單，與視訊傳送用戶端應用程式互動，為每位檢視者提供目標廣告和個人化體驗。 這些資訊清單結合了從廣告伺服器傳送的內容和廣告，並可選擇包含詳細廣告追蹤指示的中繼資料。 Primetime廣告插入支援用戶端和伺服器端廣告追蹤。

在正確設定系統後，典型的工作流程可能如下所示：

1. 用戶端應用程式會產生包含視訊串流資訊的[引導URL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)，並傳送GET要求至Primetime廣告插入。  Primetime廣告插入支援HLS和DASH，具備多種廣告訊號格式。

1. Primetime廣告插入會從發行者的CDN將內容資訊清單傳回用戶端應用程式，以回應。

1. 用戶端應用程式會在產生的資訊清單中選擇適當的串流以播放並要求插入Primetime廣告。

1. Primetime廣告插入從內容CDN擷取所要求的串流、剖析／讀取任何提示資訊、對廣告伺服器進行呼叫並視需要取代廣告插播。

1. Primetime廣告插入會重寫資源URL並偵測廣告創意是否需要轉碼，借此標準化資訊清單，請參閱[即時廣告轉碼](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md)。

1. Primetime廣告插入會擷取所需廣告創作元素，並將適當片段插入資訊清單。

1. Primetime廣告插入將最終的銜接清單（包括廣告）傳送至用戶端應用程式以供播放。

1. 您可以透過用戶端或伺服器端廣告追蹤來測量廣告傳遞和可見性，請參閱[設定廣告追蹤](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md)。

Primetime廣告插入支援大部分的HLS/DASH用戶端和播放器組態。 有關支援的特定廣告信令格式的詳細資訊，請參閱[支援的提示格式](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md)。
