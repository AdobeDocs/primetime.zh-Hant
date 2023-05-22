---
description: 清單伺服器協調提供內容、提供廣告、播放視頻和跟蹤廣告的系統。 它接收客戶視頻播放器從內容提供商接收的M3U8編碼播放清單（清單），將廣告從廣告提供商縫製到清單，並將縫製的清單傳遞給視頻播放器。 它支援客戶端和伺服器端廣告跟蹤。 它使用基於HTTP的Web服務介面進行交互。
title: 清單伺服器交互概述
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# 清單伺服器交互概述 {#overview-of-manifest-server-interactions}

清單伺服器協調提供內容、提供廣告、播放視頻和跟蹤廣告的系統。 它接收客戶視頻播放器從內容提供商接收的M3U8編碼播放清單（清單），將廣告從廣告提供商縫製到清單，並將縫製的清單傳遞給視頻播放器。 它支援客戶端和伺服器端廣告跟蹤。 它使用基於HTTP的Web服務介面進行交互。

典型配置包含：

* 黃金時段清單伺服器
* 黃金時段創意再包裝服務(CRS)
* 控制視頻播放器的客戶端
* 發佈者，通常帶有內容管理系統(CMS)
* 內容分發網路(CDN)
* 廣告伺服器
* 廣告跟蹤報告的接收器

工作流根據許多因素而變化，例如，CDN是Akamai還是客戶端正在執行廣告跟蹤。 有關客戶端廣告跟蹤的工作流圖，請參見 [客戶端跟蹤工作流](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow)。

清單伺服器通過接收和響應HTTPGET請求與視頻傳送客戶端進行交互。 響應是M3U8編碼的描述廣告縫合內容的清單，可選地包括包含詳細廣告跟蹤指令的JSON或VMAP結構(sidecar)(請參見 [檔案格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md))。

典型的工作流如下所示：

1. 發佈者將廣告伺服器的內容URL和資訊發送到客戶端。
1. 客戶端使用發佈者的資訊生成清單伺服器URL，並向該URL發送GET請求。 這稱為BootstrapURL。
1. 清單伺服器與客戶端建立會話。
1. 清單伺服器從CDN獲取內容清單，其可包括廣告中斷資訊。
1. 清單伺服器將客戶機重定向到它為客戶機生成的主/變型清單。

   >[!NOTE]
   >
   >如果BootstrapURL查詢參數包含 `pttrackingmode=simple` 或 `ptplayer=ios-mobileweb` 設定時，清單伺服器返回JSON對象中的主/變型清單URL，客戶端向該變型清單URL發送GET請求。

1. 客戶端選擇生成的變型清單中的流來播放，並將廣告資訊發送到清單伺服器。
1. 清單伺服器將客戶機提供的資訊傳遞給廣告伺服器，並從廣告伺服器接收廣告和廣告跟蹤URL。 如果提供的廣告不是HLS格式，則清單伺服器將其發送到CRS以轉換到HLS。
1. 清單伺服器將廣告縫合到內容清單中，並將新縫合清單發送到客戶端。
1. 客戶端使用縫合廣告播放內容，並在指定時間向指定的跟蹤URL發出請求。

黃金時段廣告插入支援許多視頻傳輸平台上的客戶端。 並非所有客戶端都構建在黃金時段TVSDK包上，但所有客戶端都將GET請求發送到相同的基本URL。 查詢參數通過通知清單伺服器來區分一個客戶端請求和另一個客戶端請求：

* 哪個客戶提出請求，
* 那個客戶想要的，
* 以及要提供的廣告跟蹤資訊。

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

清單伺服器使用跨源資源共用標準(CORS)。 它尋找 `Origin` 接收的請求中的標頭。 如果報頭存在，則它會回復

* `Access-Control-Allow-Origin: *`源標題中的字串`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

如果沒有，則答復如下：

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`