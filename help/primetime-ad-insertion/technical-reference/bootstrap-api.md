---
title: BootstrapAPI
description: BootstrapAPI
exl-id: bc7fe244-8664-43ac-b9a1-3967ea8749b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# BootstrapAPI {#bootstrap-api}

BootstrapAPI通常是發送到客戶端/視頻播放API的URL。  有關可配置的選項和參數，請參閱 [BootstrapAPI參數](#bootstrap-api-parameters)。

## 向清單伺服器發送命令 {#send-a-command-to-the-manifest-server}

1. 發送 `HTTP GET` 使用以下模式構建的引導URL請求：

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **檔案副檔名** 已定義。 `.m3u8` 如果目標清單是HLS, `.mpd` 目標清單在DASH中。

   * **發佈者資產ID** 必需。 Publisher特定內容的唯一ID。

   * **內容URL** 必需。 內容M3U8檔案的URL,Base64編碼為在清單伺服器URL內安全。 內容URL必須指向變型的M3U8檔案，即使只有一個比特率流。

   * **查詢參數** 這些是請求中最多樣的部分。 它們會告訴清單伺服器發出請求的客戶機類型，以及它希望清單伺服器執行什麼操作。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP與HTTPS請求**

   清單伺服器使用客戶端請求的相同HTTP協定建立URL。 如果播放器發出非安全HTTP(http)請求，則清單伺服器返回具有http協定的清單URL和審核跟蹤URL。 如果播放器建立了安全的HTTP(https)連接，清單伺服器，則它返回具有https協定的清單URL和審核跟蹤URL。

   >[!NOTE]
   >
   >清單伺服器無法更改第三方跟蹤信標的協定（HTTP或HTTPS）。 您必須聯繫內容和第三方廣告提供商，讓他們配置所需的協定。  段URL協定可以更改，但預設情況下，使用目標清單中定義的相同協定。

## BootstrapAPI參數 {#bootstrap-api-parameters}

查詢參數告訴清單伺服器客戶端發送請求的類型以及該客戶端希望清單伺服器執行的操作。 有些是必需的，有些則具有特定的可接受格式或值。
完整URL由基URL和問號組成，然後 `parameterName=value` 用和符號分隔的參數。 比如說， `Base URL?name1=value1&name2=value2& . . .&name n=value n`。

清單伺服器識別以下參數。 所有查詢字串\
參數將傳遞給ad伺服器。

| 參數 | 描述 | 格式 |
|---|---|---|
| _sid_ | 清單伺服器將用於生成會話ID的唯一ID。 | DASH/HLS都需要 |
| 活 | 通知MogineAd Insertion傳遞的內容項是即時流。  如果未傳遞此參數，Mogine Ad插入將在初始清單調用上發出次請求，以確定清單是即時還是視頻點播。<br>可能的值：<br>真實內容<br>虛<br>自動檢測省略 | HLS可選。  DASH必需 |
| z | 需要提供到黃金時段Ad Insertion的資產的區域ID。 由Adobe技術客戶經理提供。 | DASH/HLS都需要 |
| 模式 | 啟用 [部分廣告插入](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) 為即時流。<br>可能的值：<br>true啟用<br>忽略以禁用（預設禁用） | HLS/DASH |
| ptadtimeout | 如果下游提供程式響應時間過長，則允許限制總廣告解決時間。  長時間運行的響應可能會導致回放問題，這使Mighide DAI能夠在特定時間限制內強制響應。<br>可能的值：<br>數字字串（毫秒）。<br>忽略以禁用（預設禁用） | HLS/DASH |
| ptadwindows | 回望和決定窗口的持續時間（秒） — 當DVR用戶加入流時，黃金時段Ad Insertion將查找廣告提示的時間。 值為零將禁用初始清單中的中間卷和決策，而決策僅在第一次更新後恢復。 此參數對於禁用和插入只能持續幾秒鐘的會話（亦稱頻道翻轉）非常有用。<br>可能的值：<br>數字字串0-1800（預設為1800） | 僅HLS |
| p | 發佈者分配和維護的內容的唯一ID。  與Akamai Ad Scaler一起使用時需要。 | HLS/DASH |
| ptcdn | 主機轉碼資產的一個或多個CDN的清單。 有關詳細資訊，請參見 [交付和儲存](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md)。<br>可能的值：<br>akamai、level3、llnw(petting networks)、comcast。<br>預設情況下，使用黃金時段Ad InsertionCDN。 | HLS/DASH |
| ptcuformat | 要執行和決策的指定標籤格式（例如scte35）。<br>可能的值：<br>dpisimple, dpiscte35，元素<br>對於自定義提示格式，請與技術客戶代表聯繫，瞭解用於使用案例的值 | HLS/DASH |
| ptfailover | 向清單伺服器發出信號，以標識主播放清單中指定的主流和故障轉移流，並將它們視為不相交集。 這便於故障切換並防止計時錯誤。 (僅適用於AppleHLS設備。) 有關詳細資訊，請參見 [促進HLS播放器切換](hls-switching-to-failover.md) | 僅HLS |
| 多重 | 如果啟用，則對VOD資產中找到的每個可用進行單獨的廣告請求。  預設情況下，MighineAd Insertion將嘗試收集所有可用資訊，並在一個請求中將其發送到廣告伺服器。 可能的值：true可啟用， <br>忽略以禁用（預設禁用） | HLS/DASH |
| 並行流 | 允許擁有請求CMAF的播放器的客戶並行取消音頻或視頻流的混音，以確保音頻和視頻軌道中的廣告保持一致。 | 僅HLS |
| PT開關 | 啟用命名清單重寫規則和廣告獲取規則，這些規則通常由技術支援代表設定。<br>示例：adfetch_fw,cdn_akm | HLS/DASH |
| pttagds | 允許將EXT-X-DINECTION-SEQUENCE標籤注入HLS標頭。可能的值：true可啟用isomit禁用（預設禁用） | 僅HLS |
| 時間線 | 包含廣告放置和內容所需時間線的字串，該字串覆蓋內容流中的廣告斷點。 [ 查看VOD時間線格式 ] | HLS/DASH |
| pttoken | 為CDN啟用內容片段/段授權令牌保護方案<br>可能的值：<br>akamai、llnw(pettings)、ctl(centurylink)（禁用預設的標籤化） | HLS/DASH |
| 跟蹤模式 | 啟用廣告跟蹤方案。<br>可能的值：<br>客戶端廣告跟蹤簡單<br>用於伺服器端ad跟蹤的sstm<br>簡化用於混合客戶機/伺服器和廣告跟蹤（預設情況下，不執行廣告跟蹤） | HLS/DASH |
| 跟蹤位置 | 指示清單伺服器僅返回廣告跟蹤資訊。 不要在引導請求中指定此參數。<br>注：清單伺服器忽略所有傳遞的值。 但是，如果傳遞空字串或空字串，則清單伺服器將返回M3U8 | HLS/DASH<br>客戶端跟蹤 |
| pttrackingversion | 設定要返回的格式版本。<br>可能的值：<br>v1 、 v2 、 v3或vmap | HLS/DASH<br>客戶端跟蹤 |
| scte跟蹤 | 此參數向清單伺服器指示讀取M3U8的播放器需要檢索SCTE標籤資訊。<br>可能的值：<br>true或false（預設為false）<br>注：SCTE-35資料在JSONsidecar中返回，並包含以下查詢參數值組合：<br>ptcuformat=turner | 元素 | 橄欖 | DPIScte35<br>pttrackversion=v2<br>scteTracking=true<br> | 僅HLS |
| 視靶乘子 | 從即時點開始的段數預滾偏移配置為：(vetargetmultiplier * targetduration)+ vebufferlength<br>注：此參數僅適用於Live/Linear HLS流<br>可能的值：<br>數值浮點<br>（預設值）3.0 — 與HLS規範相同) | 僅HLS |
| vebufferLength | 與vetargetmuplier一起使用的從即時點開始的秒數。<br>注：此參數僅適用於Live/Linear HLS流<br>可能的值：<br>數值浮點<br>（預設值）3.0) | 僅HLS |
