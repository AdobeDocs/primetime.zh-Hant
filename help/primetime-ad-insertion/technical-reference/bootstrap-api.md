---
title: BOOTSTRAPAPI
description: BOOTSTRAPAPI
exl-id: bc7fe244-8664-43ac-b9a1-3967ea8749b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# BOOTSTRAPAPI {#bootstrap-api}

BootstrapAPI通常是傳送至使用者端/視訊播放API的URL。  如需可設定的選項和引數，請參閱 [BootstrapAPI引數](#bootstrap-api-parameters).

## 傳送命令至資訊清單伺服器 {#send-a-command-to-the-manifest-server}

1. 傳送 `HTTP GET` 要求使用下列模式建構的啟動程式URL：

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **副檔名** 已定義。 `.m3u8` 如果目標資訊清單是HLS， `.mpd` 如果目標資訊清單位於破折號中。

   * **PublisherAssetID** 必填。 特定內容的發行者唯一ID。

   * **內容URL** 必填。 內容M3U8檔案的URL，在資訊清單伺服器URL中編碼為安全的Base64。 內容URL必須指向變體M3U8檔案，即使只有一個位元速率資料流亦然。

   * **查詢引數** 這些是請求中最具多樣性的部分。 它們告訴資訊清單伺服器哪個使用者端正在提出要求，以及它想要資訊清單伺服器做什麼。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP與HTTPS要求**

   資訊清單伺服器會使用使用者端要求的相同HTTP通訊協定來建立URL。 如果播放器提出非安全HTTP (http)要求，資訊清單伺服器會傳回資訊清單URL和使用http通訊協定的稽核追蹤URL。 如果播放器透過安全HTTP (https)連線、資訊清單伺服器，會傳回資訊清單URL和使用https通訊協定的稽核追蹤URL。

   >[!NOTE]
   >
   >資訊清單伺服器無法變更第三方追蹤信標的通訊協定（HTTP或HTTPS）。 您必須連絡內容與第三方廣告提供者，讓他們設定所需的通訊協定。  區段URL通訊協定可以變更，但依預設，會使用目標資訊清單中定義的相同通訊協定。

## BootstrapAPI引數 {#bootstrap-api-parameters}

查詢引數會告知資訊清單伺服器傳送請求的使用者端型別，以及該使用者端希望資訊清單伺服器做什麼。 部分為必要專案，部分則具有可接受的特定格式或值。
完整的URL包含基底URL，後跟問號，然後 `parameterName=value` 引數以&amp;符號分隔。 例如， `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

資訊清單伺服器可辨識下列引數。 所有查詢字串\
引數會傳遞至廣告伺服器。

| 引數 | 說明 | 格式 |
|---|---|---|
| _sid_ | 資訊清單伺服器用來產生工作階段ID的唯一ID。 | 兩個破折號/水準符號均需要 |
| live | 通知PrimetimeAd Insertion傳遞的內容專案是即時資料流。  如果未傳遞此引數，Primetime廣告插入會在初始資訊清單呼叫上提出次要要求，以判斷資訊清單為即時或vod。<br>可能的值：<br>對即時內容為true<br>若為vod內容，則為false<br>省略以自動偵測 | HLS選填。  虛線必填 |
| z | 需要提供給PrimetimeAd Insertion的資產區域ID。 由您的Adobe技術客戶經理提供。 | 兩個破折號/水準符號均需要 |
| pabimode | 啟用 [部分廣告插播插入](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) 適用於即時資料流。<br>可能的值：<br>true以啟用<br>省略以停用（預設為停用） | HLS/破折號 |
| ptadtimeout | 如果下游提供者花太長的時間回應，則啟用整體廣告解析時間的限制。  長時間執行回應可能會導致播放問題，如此可讓Primetime DAI在特定時間限制內強制回應。<br>可能的值：<br>以毫秒為單位的數值字串。<br>省略以停用（預設為停用） | HLS/破折號 |
| 路徑視窗 | 回顧廣告決策視窗的持續時間（以秒為單位） — DVR使用者加入串流時，PrimetimeAd Insertion會回溯多久來尋找廣告提示。 值為零會停用初始資訊清單中的中段廣告決策，而決策只有在第一次更新後才會恢復。 此引數可用來停用可能僅持續幾秒的工作階段的廣告插入（亦稱為頻道翻轉）。<br>可能的值：<br>數值字串0-1800 （預設1800） | 僅限HLS |
| ptassetid | 由發佈者指派和維護之內容的唯一ID。  搭配Akamai Ad Scaler使用時為必要。 | HLS/破折號 |
| ptcdn | 託管轉碼資產的一或多個CDN清單。 如需詳細資訊，請參閱 [傳遞與儲存](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>可能的值：<br>akamai、level3、llnw (limelight networks)、comcast。<br>預設會使用PrimetimeAd InsertionCDN。 | HLS/破折號 |
| ptcueformat | 執行廣告決策的指定標籤格式（例如scte35）。<br>可能的值：<br>dpimple， dpiscte35， elemental<br>如需自訂提示格式，請聯絡您的技術客戶代表，以瞭解使用案例的值 | HLS/破折號 |
| ptfailover | 代表資訊清單伺服器識別主要播放清單中指定的主要和容錯移轉資料流，並將它們視為分離集。 這有助於容錯移轉並防止計時錯誤。 (僅適用於Apple HLS裝置。) 如需詳細資訊，請參閱 [促進HLS播放器切換](hls-switching-to-failover.md) | 僅限HLS |
| ptmulticall | 如果已啟用，則會針對VOD資產中的每一項可用專案提出個別的廣告請求。  根據預設，PrimetimeAd Insertion會嘗試收集所有可用的資訊，並在一個要求中將其傳送至廣告伺服器。 可能的值：true可啟用， <br>省略以停用（預設為停用） | HLS/破折號 |
| ptparallelstream | 讓客戶若有播放器要求同時使用CMAF未嵌入音訊或視訊資料流，可確保音訊和視訊曲目中的廣告保持一致。 | 僅限HLS |
| ptprotoswitch | 啟用指定的資訊清單重寫規則和廣告擷取規則，這些規則通常由您的技術支援代表設定。<br>範例： adfetch_fw， cdn_akm | HLS/破折號 |
| pttagds | 啟用將EXT-X-DISCONTINUITY-SEQUENCE標籤插入HLS標頭。可能的值：true可啟用停用（預設停用） | 僅限HLS |
| pttimeline | 字串，其中包含廣告投放和內容的所需時間軸，可覆寫內容串流中的廣告插播。 [ 請參閱VOD時間表格式 ] | HLS/破折號 |
| pttoken | 啟用CDN的內容片段/區段授權權杖保護方案<br>可能的值：<br>akamai、llnw (limelight)、ctl (centurylink) （預設代碼化為停用） | HLS/破折號 |
| pttrackingmode | 啟用廣告追蹤配置。<br>可能的值：<br>適用於使用者端廣告追蹤的簡單方法<br>用於伺服器端廣告追蹤的sstm<br>混合式使用者端/伺服器廣告追蹤的簡易步驟（預設不會執行廣告追蹤） | HLS/破折號 |
| pttrackingposition | 指示資訊清單伺服器僅傳回廣告追蹤資訊。 請勿在啟動程式要求中指定此引數。<br>注意：資訊清單伺服器會忽略所有傳遞的值。 不過，如果您傳遞null或空字串，資訊清單伺服器會傳回M3U8 | HLS/破折號<br>使用者端追蹤 |
| pttrackingversion | 設定要傳回的格式版本。<br>可能的值：<br>v1、v2、v3或vmap | HLS/破折號<br>使用者端追蹤 |
| sctetracking | 此引數會向資訊清單伺服器指出，擷取M3U8的播放器需要擷取SCTE標籤資訊。<br>可能的值：<br>true或false （預設為false）<br>注意： SCTE-35資料會以下列查詢引數值組合傳回JSON側邊欄：<br>ptcueformat=turner | 元素 | nfl | DPIScte35<br>pttrackingversion=v2<br>sctetracking=true<br> | 僅限HLS |
| vetargetmultiplier | 來自即時點的區段數使用來設定前段位移： ( vetargetmultiplier * targetduration ) + vebufferlength<br>注意：此引數僅適用於即時/線性HLS資料流<br>可能的值：<br>數值浮點數<br>（預設值： 3.0 — 與HLS規格相同） | 僅限HLS |
| vebufferLength | 從即時點開始的秒數，與vetargetmultiplier搭配使用。<br>注意：此引數僅適用於即時/線性HLS資料流<br>可能的值：<br>數值浮點數<br>（預設值： 3.0） | 僅限HLS |
