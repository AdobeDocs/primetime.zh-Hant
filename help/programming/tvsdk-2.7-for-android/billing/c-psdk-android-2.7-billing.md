---
description: 為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。
seo-description: 為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。
seo-title: 帳單量度
title: 帳單量度
uuid: 4a03995a-60f6-440e-9cdf-9c0b9c5f1d90
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 概觀 {#billing-metrics-overview}

為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。

每當播放器產生串流開始事件時，TVSDK就會定期傳送HTTP訊息至Adobe的帳單系統。 標準VOD、專業VOD（啟用中間卷廣告）和即時內容的時段稱為計費時段。 每種內容類型的預設持續時間為30分鐘，但您與Adobe的合約會決定實際值。

這些消息包含以下資訊：

* 內容類型（即時、線性或VOD）
* 內容URL
* 是否啟用廣告
* 是否啟用中轉廣告（僅限VOD）
* 流是否受DRM保護
* TVSDK版本與平台

Adobe會預先設定此安排，但您可以與Adobe Enablement代表合作，以變更安排，與您的Adobe Enablement代表合作。

若要監控TVSDK傳送至Adobe的統計資料，請從您的Adobe啟用代表取得URL，並使用網路擷取工具（例如Charles）來檢視資料。
