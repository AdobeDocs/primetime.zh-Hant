---
description: TVSDK會聯絡廣告傳送服務(例如Adobe Primetime ad decisioning)，並嘗試取得與廣告視訊資料流對應的主要播放清單檔案。 在廣告解析階段中，TVSDK會向遠端廣告傳送伺服器發出HTTP呼叫，並剖析伺服器的回應。
title: 廣告解析階段
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 廣告解析階段{#ad-resolving-phase}

TVSDK會聯絡廣告傳送服務(例如Adobe Primetime ad decisioning)，並嘗試取得與廣告視訊資料流對應的主要播放清單檔案。 在廣告解析階段中，TVSDK會向遠端廣告傳送伺服器發出HTTP呼叫，並剖析伺服器的回應。

TVSDK支援下列型別的廣告提供者：

* 中繼資料廣告提供者

  廣告資料會以純文字JSON檔案編碼。
* Primetime廣告決策廣告提供者

  TVSDK會傳送要求（包括一組目標定位引數和資產識別碼）至Primetime ad decisioning後端伺服器。 Primetime廣告決策會以包含所需廣告資訊的SMIL （同步多媒體整合語言）檔案回應。
* 自訂廣告標籤提供者

  處理從伺服器端將廣告燒錄到串流中的情況。 TVSDK不會執行實際的廣告插入，但需要追蹤插入伺服器端的廣告。 此提供者會設定TVSDK用來執行廣告追蹤的廣告標籤。

在此階段可能會發生下列其中一種容錯移轉情況：

* 無法擷取資料，原因包括缺乏連線或伺服器端錯誤，例如找不到資源等。
* 已擷取資料，但格式無效。

  例如，發生此狀況可能是因為剖析傳入資料失敗。

TVSDK會發出有關錯誤的警告通知，並繼續處理。
