---
title: 引導API
description: '引導API '
translation-type: tm+mt
source-git-commit: bf99c76bbbb67560adc675cf84297b8d3b04e19d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# 引導API {#bootstrap-api}

引導API通常是傳送至用戶端／視訊播放API的URL。  有關可配置的選項和參數，請參閱[引導API參數](#bootstrap-api-parameters)。

## 將命令發送到Manifest伺服器{#send-a-command-to-the-manifest-server}

1. 傳送`HTTP GET`請求，請求使用下列模式建構的引導URL:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **副檔名** 已定義。`.m3u8` 如果目標清單是HLS, `.mpd` 如果目標清單在DASH中。

   * **需** 要PublisherAssetIDR。特定內容的發行者唯一ID。

   * **需要** 內容URLRred。內容M3U8檔案的URL,Base64編碼為在資訊清單伺服器URL中安全。 內容URL必須指向變數的M3U8檔案，即使只有一個位元速率串流亦然。

   * **查詢** 參數這些參數構成請求中最多變的部分。他們會告訴資訊清單伺服器提出要求的用戶端類型，以及資訊清單伺服器要做什麼。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP與HTTPS要求**

   資訊清單伺服器會使用與用戶端要求相同的HTTP通訊協定來建立URL。 如果播放器發出非安全的HTTP(http)要求，資訊清單伺服器會以http通訊協定傳回資訊清單URL和Auditude追蹤URL。 如果播放器建立安全的HTTP(https)連線，manifest伺服器，則會傳回具有https通訊協定的資訊清單URL和Auditude追蹤URL。

   >[!NOTE]
   >
   >資訊清單伺服器無法變更第三方追蹤信標的通訊協定（HTTP或HTTPS）。 您必須聯絡內容和第三方廣告供應商，讓他們設定所需的通訊協定。  區段URL通訊協定可以變更，但依預設，使用與目標清單中定義的相同通訊協定。

## 引導API參數{#bootstrap-api-parameters}

查詢參數會告訴資訊清單伺服器，用戶端傳送請求的類型，以及該用戶端希望資訊清單伺服器執行的動作。 有些是必要的，有些則具有特定的可接受格式或值。
完整的URL由基本URL和問號組成，然後由&amp;符號分隔的`parameterName=value`引數。 例如，`Base URL?name1=value1&name2=value2& . . .&name n=value n`。

資訊清單伺服器可識別下列參數。 所有查詢字串\
參數會傳遞至廣告伺服器。

| 參數 | 描述 | 格式 |
|---|---|---|
| _sid_ | 資訊清單伺服器將用來產生工作階段ID的唯一ID。 | DASH/HLS都需要 |
| live | 通知Primetime廣告插入，傳遞的內容項目是即時串流。  如果未傳遞此參數，Primetime廣告插入會在初始資訊清單呼叫上提出次要請求，以判斷資訊清單是即時或vod。<br>可能的值：<br>即時內容<br>為true對vod內容<br>為false，以自動偵測 | HLS的可選項。  DASH必需 |
| z | 需要提供給Primetime廣告插入的資產的區域ID。 由您的Adobe技術客戶經理提供。 | DASH/HLS都需要 |
| pabimode | 啟用「即時」串流的[部分廣告插入](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support)。<br>可能的值： <br>true to <br>enableimot to disable（預設禁用） | HLS/DASH |
| ptadtimeout | 允許在下游提供者響應時間太長時限限制整體廣告解析時間。  長時間執行的回應可能會造成播放問題，這可讓Primetime DAI在特定時限內強制回應。<br>可能的值：<br>以毫秒為單位的數值字串。<br>省略以停用（預設為停用） | HLS/DASH |
| ptadwindow | 回顧廣告決策視窗的持續時間（以秒為單位）—當DVR使用者加入串流時，「黃金時段廣告插入」會在多長時間內尋找廣告提示。 若值為零，則會停用初始資訊清單中的中段廣告決策，且決策只會在第一次更新後繼續。 此參數對於停用可持續數秒（亦即頻道轉換）的作業的廣告插入很有用。<br>可能的值：<br>數值字串0-1800（預設值1800） | 僅限HLS |
| ptassetid | 發佈者指派和維護之內容的唯一ID。  與Akamai Ad Scaler搭配使用時需要。 | HLS/DASH |
| ptcdn | 托管已轉碼資產的一或多個CDN清單。 如需詳細資訊，請參閱[傳送與儲存](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md)。<br>可能的值：<br>akamai、level3、llnw(limelight networks)、comcast。<br>依預設，會使用Primetime廣告插入CDN。 | HLS/DASH |
| ptcueformat | 要執行廣告決策的指定標籤格式（例如scte35）。<br>可能的值：<br>dpisimple、dpiscte35、<br>elementalFor custom cue formats，請聯絡您的技術帳戶代表，以取得用於使用案例的值 | HLS/DASH |
| ptfailover | 向資訊清單伺服器發出訊號，以識別主播放清單中指定的主要和容錯串流，並將它們視為不相交集。 這有助於故障切換並防止計時錯誤。 （僅適用於Apple HLS裝置）。 如需詳細資訊，請參閱[促進HLS播放器切換](hls-switching-to-failover.md) | 僅限HLS |
| ptmulticall | 如果啟用，則會針對VOD資產中的每個可用項目提出個別的廣告請求。  依預設，「Primetime廣告插入」會嘗試收集所有可用資訊，並在單一請求中將其傳送至廣告伺服器。 可能的值：true to enable, <br>imot to disable（預設禁用） | HLS/DASH |
| ptarallew | 讓擁有要求CMAF的播放器的客戶可同時去除混音音或視訊串流，以確保音訊和視訊軌中的廣告一致。 | 僅限HLS |
| ptprotoswitch | 啟用指名的資訊清單重寫規則和廣告擷取規則，通常由您的技術支援代表設定。<br>範例：adfetch_fw, cdn_akm | HLS/DASH |
| pttagds | 啟用將EXT-X-DINSUCTION-SEQUENCE標籤注入HLS標頭。可能的值：true to enableimot to disable（預設禁用） | 僅限HLS |
| pttimelime | 包含廣告位置和內容所需時間軸的字串，會覆寫內容串流中的廣告分段。 [ 請參閱VOD時間軸格式  ] | HLS/DASH |
| pttoken | 為CDN啟用內容片段／區段授權Token保護方案<br>可能的值：<br>akamai、llnw(limelight)、ctl(centurylink)（預設Tokenization已停用） | HLS/DASH |
| pttrackingmode | 啟用廣告追蹤方案。<br>可能的值：<br>用於用戶端和追蹤的<br>stm簡單適用於伺服器端和追蹤的<br>stm簡單適用於混合用戶端／伺服器廣告追蹤（預設不執行廣告追蹤） | HLS/DASH |
| pttrackingposition | 指示資訊清單伺服器僅傳回廣告追蹤資訊。 請勿在引導請求中指定此參數。<br>注意：資訊清單伺服器會忽略所有傳遞的值。不過，如果您傳遞空字串或空字串，資訊清單伺服器會傳回M3U8 | HLS/DASH<br>用戶端追蹤 |
| pttrackingversion | 設定要返回的格式版本。<br>可能的<br>值：v1、v2、v3或vmap | HLS/DASH<br>用戶端追蹤 |
| scteTracking | 此參數向資訊清單伺服器指出擷取M3U8的播放器需要擷取SCTE標籤資訊。<br>可能的值：<br>true或false（預設為false）<br>注意：SCTE-35資料會在JSONsidecar中傳回，並包含以下查詢參數值的組合：<br>ptcueformat=turner | 元素 | nfl | DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | 僅限HLS |
| vetargetmultipher | 來自活動點的段數預滾偏移是使用下列方式配置的：(vetargetmultipher * targetduration)+ vebufferlength<br>注意：此參數僅適用於即時／線性HLS流<br>可能值：<br>數字浮點<br>(預設值：3.0 —— 與HLS規範相同) | 僅限HLS |
| vebufferLength | 從即時點開始的秒數，與vetarget乘數一起使用。<br>注意：此參數僅適用於Live/Linear HLS串流<br>可能的值：<br>數值float<br>(預設值：3.0) | 僅限HLS |
