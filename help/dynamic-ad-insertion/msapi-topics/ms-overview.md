---
description: 資訊清單伺服器可協調提供內容、提供廣告、播放視訊和追蹤廣告的系統。 它接收客戶視訊播放器從內容提供者接收的M3U8編碼播放清單（清單），將廣告提供者的廣告插入清單，並將銜接清單傳遞給視訊播放器。 它支援用戶端和伺服器端廣告追蹤。 它使用以HTTP為基礎的web service介面進行互動。
seo-description: 資訊清單伺服器可協調提供內容、提供廣告、播放視訊和追蹤廣告的系統。 它接收客戶視訊播放器從內容提供者接收的M3U8編碼播放清單（清單），將廣告提供者的廣告插入清單，並將銜接清單傳遞給視訊播放器。 它支援用戶端和伺服器端廣告追蹤。 它使用以HTTP為基礎的web service介面進行互動。
seo-title: 資訊清單伺服器互動概觀
title: 資訊清單伺服器互動概觀
uuid: 3e314a45-a4dd-492f-8915-19224a8fbbc7
translation-type: tm+mt
source-git-commit: 9dc8498593a1d70918b66016e429eb013cdc61f7

---


# 資訊清單伺服器互動概觀 {#overview-of-manifest-server-interactions}

資訊清單伺服器可協調提供內容、提供廣告、播放視訊和追蹤廣告的系統。 它接收客戶視訊播放器從內容提供者接收的M3U8編碼播放清單（清單），將廣告提供者的廣告插入清單，並將銜接清單傳遞給視訊播放器。 它支援用戶端和伺服器端廣告追蹤。 它使用以HTTP為基礎的web service介面進行互動。

典型配置包含：

* Primetime資訊清單伺服器
* Primetime Creative重新封裝服務(CRS)
* 控制視頻播放器的客戶端
* 發佈者，通常具有內容管理系統(CMS)
* 內容傳送網路(CDN)
* 廣告伺服器
* 廣告追蹤報表的接收者

工作流程會根據許多因素而有所不同，例如CDN是Akamai，或是用戶端正在執行廣告追蹤。 如需用戶端廣告追蹤工作流程的圖表，請參 [閱用戶端追蹤工作流程](../msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow)。

資訊清單伺服器會接收並回應HTTP GET要求，以與視訊傳送用戶端互動。 這些回應是M3U8編碼的資訊清單，描述廣告銜接內容，可選擇包含JSON或VMAP結構(sidecar)，其中包含詳細的廣告追蹤指示(請參閱 [檔案格式](../msapi-topics/ms-list-file-formats/ms-api-file-formats.md))。

典型的工作流程如下所示：

1. 發佈者會傳送廣告伺服器的內容URL和資訊給用戶端。
1. 用戶端使用發佈者的資訊來產生資訊清單伺服器URL，並傳送GET要求至該URL。 這稱為引導URL。
1. 資訊清單伺服器與用戶端建立工作階段。
1. 資訊清單伺服器從CDN取得內容清單，其可包含廣告中斷資訊。
1. 資訊清單伺服器將用戶端重新導向至其為用戶端產生的主／變型資訊清單。

   >[!NOTE]
   >
   >如果引導URL查詢參數包含 `pttrackingmode=simple``ptplayer=ios-mobileweb` 或設定，則資訊清單伺服器會傳回JSON物件中的主／變型資訊清單URL，而用戶端會傳送GET要求至該變型資訊清單URL。

1. 客戶端選擇所生成的變型清單中的流來播放，向清單伺服器發送廣告資訊。
1. 資訊清單伺服器將用戶端提供的資訊傳送至廣告伺服器，並從廣告伺服器接收廣告和廣告追蹤URL。 如果提供的廣告不是HLS格式，資訊清單伺服器會將其傳送至CRS，以轉換至HLS。
1. 資訊清單伺服器將廣告接合到內容資訊清單中，並將新的接合資訊清單傳送至用戶端。
1. 用戶端會以銜接廣告來播放內容，並在指定的時間要求指定的追蹤URL。

Primetime廣告插入支援許多視訊傳送平台的客戶。 並非所有用戶端都是以Primetime TVSDK套件為基礎，但所有用戶端都會將GET要求傳送至相同的基本URL。 查詢參數會通知資訊清單伺服器：

* 是哪位客戶提出要求，
* 那個客戶想要什麼，
* 以及要提供的廣告追蹤資訊。

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

資訊清單伺服器使用跨原始資源共用標準(CORS)。 它會在收到的 `Origin` 請求中尋找標題。 如果標題存在，則會以

* `Access-Control-Allow-Origin: *`來源標題的字串`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

如果不是，則會回覆：

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`