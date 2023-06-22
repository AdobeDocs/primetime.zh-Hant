---
description: 為因應客戶只想依使用量付款，而不想依實際使用量支付固定費率的需求，Adobe會收集使用量度並使用這些量度來決定向客戶收費的金額。
title: 計費量度
exl-id: f4200573-571f-4ed3-be8c-08b72d4f9e0e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 概觀 {#billing-metrics-overview}

為因應客戶只想依使用量付款，而不想依實際使用量支付固定費率的需求，Adobe會收集使用量度並使用這些量度來決定向客戶收費的金額。

每次播放器產生資料流開始事件時，瀏覽器TVSDK就會開始定期傳送HTTP訊息至Adobe的計費系統。 期間（稱為可計費期間）在標準VOD、pro VOD （啟用中段廣告）和即時內容中可能不同。 每種內容型別的預設持續時間為30分鐘，但您的Adobe合約會決定實際值。

訊息包含下列資訊：

* 內容型別（即時、線性或VOD）
* 內容URL
* 是否啟用廣告
* 是否啟用中段廣告（僅限VOD）
* 資料流是否受DRM保護
* 瀏覽器TVSDK版本和平台

Adobe會預先設定此安排，但如果您想要變更安排，請與您的Adobe啟用代表合作。

若要監視Browser TVSDK傳送至Adobe的統計資料，請從您的Adobe啟用代表取得URL，然後使用網路擷取工具（例如Charles）來檢視資料。
