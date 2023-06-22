---
title: 開始使用Adobe PrimetimeAd Insertion
description: Adobe PrimetimeAd Insertion快速入門
exl-id: 629ea2a5-1b50-4451-a478-95d02f192145
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 開始使用Adobe PrimetimeAd Insertion {#ptai-get-started}

PrimetimeAd Insertion會協調提供內容和廣告的系統，以建立個人化的串流廣告體驗，然後追蹤廣告商的廣告播放。

PrimetimeAd Insertion會透過重新撰寫視訊資訊清單來與視訊傳送使用者端應用程式互動，以為每個檢視者提供目標廣告和個人化體驗。 這些資訊清單結合了從廣告伺服器傳送的內容和廣告，並可選擇包含詳細廣告追蹤指示的中繼資料。 PrimetimeAd Insertion同時支援使用者端和伺服器端的廣告追蹤。

正確設定系統後，典型的工作流程可能如下所示：

1. 使用者端應用程式會產生 [BOOTSTRAPURL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) 內含視訊串流相關資訊，並傳送請GET至PrimetimeAd Insertion。  PrimetimeAd Insertion支援多種廣告訊號格式的HLS和DASH。

1. PrimetimeAd Insertion會將內容資訊清單從發行者的CDN傳回使用者端應用程式，以回應。

1. 使用者端應用程式會在產生的資訊清單中選擇要播放的適當串流，並向PrimetimeAd Insertion提出要求。

1. PrimetimeAd Insertion會從內容CDN擷取要求的資料流、解析/讀取任何提示資訊、呼叫廣告伺服器並在必要時取代廣告插播。

1. PrimetimeAd Insertion會重寫資源URL並偵測廣告創意內容是否需要轉碼，以標準化資訊清單，請參閱 [即時廣告轉碼](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md).

1. PrimetimeAd Insertion會擷取所需的廣告創意，並將適當的片段插入資訊清單中。

1. PrimetimeAd Insertion會將最終彙整的資訊清單（包括廣告）提供給使用者端應用程式進行播放。

1. 廣告傳遞和可檢視度可以透過使用者端或伺服器端廣告追蹤來測量，請參閱 [設定廣告追蹤](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md).

PrimetimeAd Insertion支援大部分的HLS/DASH使用者端和播放器設定。 如需有關支援的特定廣告訊號格式的詳細資訊，請參閱 [支援的提示格式](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md).
