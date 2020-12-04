---
description: 為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。
seo-description: 為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。
seo-title: 帳單量度
title: 帳單量度
uuid: e09b77b3-89d3-44d6-be4e-e1612fbf89fc
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 概述{#billing-metrics-overview}

為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。

每當播放器產生串流開始事件時，瀏覽器TVSDK就會定期傳送HTTP訊息至Adobe的帳單系統。 標準VOD、專業VOD（啟用中間卷廣告）和即時內容的時段稱為計費時段。 每種內容類型的預設持續時間為30分鐘，但您與Adobe的合約會決定實際值。

這些消息包含以下資訊：

* 內容類型（即時、線性或VOD）
* 內容URL
* 是否啟用廣告
* 是否啟用中轉廣告（僅限VOD）
* 流是否受DRM保護
* 瀏覽器TVSDK版本與平台

Adobe會預先設定此安排，但如果您想要變更安排，請與您的Adobe啟用代表合作。

若要監控瀏覽器TVSDK傳送至Adobe的統計資料，請從您的Adobe啟用代表取得URL，並使用網路擷取工具（例如Charles）來查看資料。
