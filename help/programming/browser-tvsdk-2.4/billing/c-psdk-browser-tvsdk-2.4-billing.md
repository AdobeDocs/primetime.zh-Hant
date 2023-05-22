---
description: 為了適應那些只想按使用付費而不是按固定費率付費的客戶，Adobe收集使用量度，並使用這些度量來確定向客戶收取的費用。
title: 計費度量
exl-id: f4200573-571f-4ed3-be8c-08b72d4f9e0e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 概述 {#billing-metrics-overview}

為了適應那些只想按使用付費而不是按固定費率付費的客戶，Adobe收集使用量度，並使用這些度量來確定向客戶收取的費用。

每次播放器生成流啟動事件時，瀏覽器TVSDK開始定期向Adobe的計費系統發送HTTP消息。 該週期稱為可計費持續時間，對於標準VOD、pro VOD（啟用中間廣告）和即時內容可以不同。 每種內容類型的預設持續時間為30分鐘，但您與Adobe的合同將確定實際值。

這些消息包含以下資訊：

* 內容類型（即時、線性或VOD）
* 內容URL
* 是否啟用廣告
* 是否啟用中間卷廣告（僅VOD）
* 流是否受DRM保護
* 瀏覽器TVSDK版本和平台

Adobe預先配置此安排，但如果要更改此安排，請與您的Adobe支援代表合作。

要監視瀏覽器TVSDK發送到Adobe的統計資訊，請從Adobe啟用代表處獲取URL，然後使用網路捕獲工具（例如Charles）查看資料。
