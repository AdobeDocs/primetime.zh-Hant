---
title: 開始使用Adobe PrimetimeAd Insertion
description: Adobe PrimetimeAd Insertion
exl-id: 629ea2a5-1b50-4451-a478-95d02f192145
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 開始使用Adobe PrimetimeAd Insertion {#ptai-get-started}

黃金時段Ad Insertion協調提供內容和廣告的系統，以建立個性化的流中廣告體驗，然後跟蹤廣告商的廣告回放。

黃金時段Ad Insertion通過重新編寫視頻清單與視頻傳送客戶端應用程式交互，以便為每個觀看者提供有針對性的廣告和個性化體驗。 這些清單將從廣告伺服器傳送的內容和廣告組合在一起，並可選擇包括包含詳細廣告跟蹤指令的元資料。 黃金時段Ad Insertion支援客戶端和伺服器端廣告跟蹤。

正確設定系統後，典型工作流可能如下所示：

1. 客戶端應用程式生成 [BootstrapURL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) 提供有關視頻流的資訊，並向黃金時段Ad Insertion發送GET請求。  黃金時段Ad Insertion支援HLS和DASH，它們具有各種廣告信令格式。

1. 黃金時段Ad Insertion通過將內容清單從發佈者的CDN發回到客戶端應用程式來響應。

1. 客戶端應用程式選擇生成的清單中的適當流來播放並請求黃金時段Ad Insertion。

1. 黃金時段Ad Insertion從內容CDN中提取所請求的流，解析/讀取任何提示資訊，對廣告伺服器進行呼叫並根據需要替換廣告分段。

1. 黃金時段Ad Insertion通過重寫資源URL並檢測廣告創意是否需要轉碼來規範清單，請參閱 [即時廣告轉碼](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md)。

1. 黃金時段Ad Insertion提取所需廣告創意並將適當片段插入清單。

1. 黃金時段Ad Insertion將包括廣告在內的最終縫合清單遞送至客戶端應用程式以進行回放。

1. 可以通過客戶端或伺服器端廣告跟蹤來測量廣告交付和可查看性，請參見 [設定廣告跟蹤](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md)。

黃金時段Ad Insertion支援大多數HLS/DASH客戶端和播放器配置。 有關支援的特定廣告信令格式的詳細資訊，請參閱 [支援的提示格式](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md)。
