---
description: 資訊清單伺服器會協調提供內容、提供廣告、播放視訊和追蹤廣告的系統。 它會接收使用者端視訊播放器從內容提供者接收的M3U8編碼播放清單（資訊清單）、將廣告提供者的廣告拼接至資訊清單，並將拼接的資訊清單傳遞至視訊播放器。 它同時支援使用者端和伺服器端的廣告追蹤。 它會使用HTTP型Web服務介面進行互動。
title: 資訊清單伺服器互動概述
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# 資訊清單伺服器互動概述 {#overview-of-manifest-server-interactions}

資訊清單伺服器會協調提供內容、提供廣告、播放視訊和追蹤廣告的系統。 它會接收使用者端視訊播放器從內容提供者接收的M3U8編碼播放清單（資訊清單）、將廣告提供者的廣告拼接至資訊清單，並將拼接的資訊清單傳遞至視訊播放器。 它同時支援使用者端和伺服器端的廣告追蹤。 它會使用HTTP型Web服務介面進行互動。

典型設定包含：

* Primetime資訊清單伺服器
* Primetime Creative Repackaging Service (CRS)
* 控制視訊播放器的使用者端
* 發行者，通常具有內容管理系統(CMS)
* 內容傳遞網路(CDN)
* 廣告伺服器
* 廣告追蹤報表的接收者

工作流程會因數種因素而異，例如CDN是否為Akamai，或使用者端是否正在執行廣告追蹤。 如需使用者端廣告追蹤的工作流程圖表，請參閱 [使用者端追蹤工作流程](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

資訊清單伺服器會接收並回應HTTPGET要求，與視訊傳遞使用者端互動。 回應是M3U8編碼的資訊清單，說明廣告拼接內容，選擇性地包括包含詳細廣告追蹤指示的JSON或VMAP結構（側欄） (請參閱 [檔案格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md))。

典型的工作流程如下所示：

1. 發佈者會將廣告伺服器的內容URL和資訊傳送給使用者端。
1. 使用者端會使用來自發佈者的資訊來產生資訊清單伺服器URL，並傳送GET要求至該URL。 這稱為BootstrapURL。
1. 資訊清單伺服器會建立與使用者端的工作階段。
1. 資訊清單伺服器會從CDN取得內容資訊清單，其中可能包含廣告插播資訊。
1. 資訊清單伺服器會將使用者端重新導向至它為使用者端產生的主要/變體資訊清單。

   >[!NOTE]
   >
   >如果BootstrapURL查詢引數包含 `pttrackingmode=simple` 或 `ptplayer=ios-mobileweb` 設定時，資訊清單伺服器會傳回JSON物件中的主要/變體資訊清單URL，而使用者端會傳送GET要求給該變體資訊清單URL。

1. 使用者端選擇播放產生的變體資訊清單中的資料流，將廣告資訊傳送至資訊清單伺服器。
1. 資訊清單伺服器會將使用者端提供的資訊傳遞至廣告伺服器，並從廣告伺服器接收廣告和廣告追蹤URL。 如果提供的廣告不是HLS格式，資訊清單伺服器會將其傳送至CRS以轉換為HLS。
1. 資訊清單伺服器會將廣告拼接至內容資訊清單，並將新拼接的資訊清單傳送給使用者端。
1. 使用者端播放內含拼接廣告的內容，並在指定時間向指定的追蹤URL提出要求。

Primetime廣告插入支援許多視訊傳送平台上的使用者端。 並非所有使用者端都建立在Primetime TVSDK套件上，但所有使用者端都會將GET要求傳送至相同的基本URL。 查詢引數可告知資訊清單伺服器，以區分不同的使用者端要求：

* 哪個使用者端正在提出要求，
* 客戶想要什麼，
* 以及要提供哪些廣告追蹤資訊。

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

資訊清單伺服器使用跨原始資源共用標準(CORS)。 它會尋找 `Origin` 標頭。 如果標題存在，則會回覆

* `Access-Control-Allow-Origin: *`來自Origin標頭的字串`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

如果沒有，則會回覆為：

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`