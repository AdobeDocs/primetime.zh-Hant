---
description: 查詢參數會告訴資訊清單伺服器，用戶端傳送請求的類型，以及該用戶端希望資訊清單伺服器執行的動作。 有些是必要的，有些則具有特定的可接受格式或值。
seo-description: 查詢參數會告訴資訊清單伺服器，用戶端傳送請求的類型，以及該用戶端希望資訊清單伺服器執行的動作。 有些是必要的，有些則具有特定的可接受格式或值。
seo-title: 資訊清單伺服器查詢參數
title: 資訊清單伺服器查詢參數
uuid: 03632da3-ae20-427c-bd24-4794ab627cc8
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# 資訊清單伺服器查詢參數 {#manifest-server-query-parameters}

查詢參數會告訴資訊清單伺服器，用戶端傳送請求的類型，以及該用戶端希望資訊清單伺服器執行的動作。 有些是必要的，有些則具有特定的可接受格式或值。

完整的URL包含基本URL，後面接著問號，然後是引數， `parameterName=value` 以&amp;符號分隔： `Base URL?name1=value1&name2=value2& . . .&name n=value n`

## 可識別的參數 {#section_072845B7FA94468C8068E9092983C9E6}

資訊清單伺服器可識別下列參數。 它會處理它們，或將它們連同所有無法識別的參數傳遞至廣告伺服器。

| Key | 說明 | 必要 | 有效值 |
|--- |--- |--- |--- |
| `__sid__` | 資訊清單伺服器用來產生工作階段ID的唯一ID。 | 是 | 字母數字 |
| g | 用戶端裝置類型 | 當定位規則取決於裝置類型時 | 請參閱客戶 [端類型清單](https://adobeprimetime.zendesk.com) （需要Zendesk存取） |
| k | 自訂廣告定位的關鍵字 | 否 | 格式為key1=value1;key2=value2；的URL-safe字串。.. |
| u | Primetime廣告插入資產ID。 | 是 | MD5雜湊值 |
| z | 資產的Primetime廣告插入區域ID。 | 是 | 整數 |
| enableC3 | 客戶端位於C3窗口中。 如果為true，則僅替換本地可用；否則，請更換所有可用。 | 否 | 布林值 |
| live | 指出內容是即時或VOD（視訊隨選）串流。 | Akamai Ad Scaler或iOS Safari用戶端 | 布林值 |
| pabimode | [啟用部分廣告插入支援](../../msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) ：若為true則啟用；若為false則啟動停用 | 否（預設為停用） | 開始、true或false |
| ptadwindow | 廣告拼接視窗的持續時間（秒）:當DVR使用者加入串流時，要尋找廣告的距離。 | 否（預設值= 1800） | 0至1800 |
| ptassetid | 發佈者指派和維護之內容的唯一ID。 | Akamai Ad Scaler | URL安全字串 |
| ptcdn | 托管已轉碼資產的一或多個CDN清單。 請參 [閱多CDN支援](../../creative-repackaging-service/multi-cdn-supportt.md)。 | 否（預設值=Akamai） | 範例：Akamai、Level3、Limelight、Comcast |
| ptcueformat | M3U8中顯示的自訂廣告提示格式名稱。 | 否 | DPISimple、DPIScte35、Elemental、NBC、NFL或Turner |
| ptfailover | 向資訊清單伺服器發出訊號，以識別主播放清單中指定的主要和容錯串流，並將它們視為不相交集。 這有助於故障切換並防止計時錯誤。 （僅適用於Apple HLS裝置）。 請參閱 [促進HLS播放器切換](../../msapi-topics/ms-insert-ads/hls-switching-to-failover.md) 。 | 否 | true |
| ptmulticall | 若設為true，則會進行多次Auditude廣告呼叫FER;每個廣告插播各一個。  如果缺席或設為false，則會針對FER發出一個廣告呼叫給auditude。 | 否 | 布林值附註： 下列需求： <ul><li>ptcueformat參數必須設定為nbc</li><li>pttimeline參數會被忽略。</li></ul> |
| ptplayer | 播放程式提出要求。 | iOS/Safari | ios-mobileweb |
| ptrendition | 廣告插入自動產生，Akamai使用。 請勿新增或移除。 | Akamai Ad Scaler |  |
| pttagds | 啟 [用EXT-X-不連續序列標籤](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | 否 | true - manifest伺服器在其傳送的每個m3u8檔案中，在內容之前加入序列標籤；如果參數不存在或不是true，則manifest伺服器不包含序列標籤。 |
| pttimelime | 包含廣告位置和內容所需時間軸的字串，會覆寫內容串流中的廣告分段。 | 否 | VOD時間軸(請參 [閱VOD時間軸格式](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)) |
| pttoken | 啟用TS段授權令牌注意： 僅支援Akamai CDN Token | 針對TS區段授權Token | 布林值 |
| pttrackingmode | 啟用廣告追蹤；自訂用戶端（簡單）、伺服器端(sstm)或混合（簡單）。 | 否 | simple 、 sstm或simplesstm注意： 如果未包含此參數，則#EX-X-MARKER會插入資訊清單中。 請參 [閱EXT-X-MARKER指令](../../msapi-topics/ms-at-effectiveness/ms-api-playlists.md)。 |
| pttrackingposition | 指示資訊清單伺服器僅傳回廣告追蹤資訊。 請勿在引導請求中指定此參數。 | 用戶端追蹤 | 字母數字附註： 資訊清單伺服器會忽略所有傳遞的值。 不過，如果您傳遞空字串或空字串，資訊清單伺服器會傳回M3U8，而非追蹤資訊。 |
| pttrackingversion | 用戶端追蹤資訊的格式版本。 | 用戶端追蹤 | v1、v2、v3或vmap |
| scteTracking | 在JSON V2附屬內容中擷取SCTE追蹤資訊之前，請先擷取M3U8。  <br/>此參數向資訊清單伺服器指出擷取M3U8的播放器需要擷取SCTE標籤資訊。 | 否(預設值： false) | 真或假附註： SCTE-35資料會在JSONsidecar中傳回，並包含下列查詢參數值組合： <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35` </li><li>pttrackingversion=v2 </li><li>scteTracking=true</li></ul> |
| vetargetmultipher | 來自活動點的段數預滾偏移是使用下列方式配置的：  `(  vetargetmultiplier  *  targetduration ) +  vebufferlength`  <br/><br/>**注意**: 僅限即時／線性 | 否(預設值： 3.0) | 浮點 |
| vebufferLength | 從即時點開始的秒數附註： 僅限即時／線性 | 否(預設值： 3.0) | 浮點 |
