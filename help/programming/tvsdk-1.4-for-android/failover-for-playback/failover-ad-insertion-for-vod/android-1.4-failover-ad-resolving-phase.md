---
description: TVSDK會連絡廣告傳送服務，例如Adobe Primetime廣告決策，並嘗試取得與廣告的視訊串流對應的主要播放清單檔案。 在廣告解析階段，TVSDK會對遠端廣告傳送伺服器進行HTTP呼叫，並分析伺服器的回應。
title: 廣告解析階段
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 廣告分辨階段{#ad-resolving-phase}

TVSDK會連絡廣告傳送服務，例如Adobe Primetime廣告決策，並嘗試取得與廣告的視訊串流對應的主要播放清單檔案。 在廣告解析階段，TVSDK會對遠端廣告傳送伺服器進行HTTP呼叫，並分析伺服器的回應。

TVSDK支援下列類型的廣告提供者：

* 中繼資料廣告提供者

   廣告資料會編碼為純文字JSON檔案。
* Primetime廣告決策廣告供應商

   TVSDK會傳送要求（包括一組定位參數和資產識別碼）至Primetime廣告決策後端伺服器。 Primetime廣告決策會以包含所需廣告資訊的SMIL（同步化多媒體整合語言）檔案做出回應。
* 自訂廣告標籤提供者

   處理廣告從伺服器端燒錄至串流的情況。 TVSDK不會執行實際的廣告插入，但需要追蹤在伺服器端插入的廣告。 此提供者會設定TVSDK用來執行廣告追蹤的廣告標籤。

在此階段中，可能會發生以下故障切換情形之一：

* 由於缺乏連接或伺服器端錯誤（例如找不到資源等）等原因，無法擷取資料。
* 已擷取資料，但格式無效。

   這可能是因為，例如，對入站資料的解析失敗。

TVSDK會針對錯誤發出警告通知，並繼續處理。
