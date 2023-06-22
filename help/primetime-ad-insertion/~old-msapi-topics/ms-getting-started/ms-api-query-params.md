---
title: 資訊清單伺服器查詢引數
description: 查詢引數會告知資訊清單伺服器傳送請求的使用者端型別，以及該使用者端希望資訊清單伺服器做什麼。 部分為必要專案，部分則具有可接受的特定格式或值。
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# 資訊清單伺服器查詢引數 {#ms-query-params}

查詢引數會告知資訊清單伺服器傳送請求的使用者端型別，以及該使用者端希望資訊清單伺服器做什麼。 部分為必要專案，部分則具有可接受的特定格式或值。

完整的URL包含基底URL，後跟問號，然後 `parameterName=value` 引數，以&amp;符號分隔： `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## 已識別的引數 {#section_072845B7FA94468C8068E9092983C9E6}

資訊清單伺服器可辨識下列引數。 它會處理這些引數，或連同所有無法辨識的引數一起傳送至廣告伺服器。

| 金鑰 | 說明 | 必填 | 有效值 |
|---|---|---|---|
| `__sid__` | 資訊清單伺服器用來產生工作階段ID的唯一ID。 | 是 | 英數字元 |
| g | 使用者端裝置型別 | 當鎖定目標規則取決於裝置型別時 | 檢視清單于 [使用者端型別](https://adobeprimetime.zendesk.com). 需要Zendesk存取權。 |
| k | 自訂廣告目標定位的關鍵字 | 否 | 格式中的URL安全字串 `key1=value1;key2=value2;. . .` |
| u | Primetime廣告插入資產ID。 | 是 | MD5雜湊值 |
| z | 資產的Primetime廣告插入區域ID。 | 是 | 整數 |
| enableC3 | 使用者端在C3視窗中。 如果為true，則僅取代本機可用；否則，取代所有可用。 | 否 | 布林值 |
| live | 指出內容為即時或VOD （視訊隨選）資料流。 | Akamai Ad Scaler或iOS Safari使用者端。 | 布林值 |
| `pabimode` | [啟用部分廣告插播插入](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) 支援。 <br> 如果true或start則啟用。<br> 若為false則停用。 | 否（預設為停用） | start、true或false |
| `ptadwindow` | 廣告拼接視窗的持續時間（秒）：當DVR使用者加入資料流時，要回顧多久才會尋找廣告。 | 否（預設= 1800） | 0至1800 |
| `ptassetid` | 由發佈者指派和維護之內容的唯一ID。 | Akamai廣告縮放器 | URL安全字串 |
| `ptcdn` | 託管轉碼資產的一或多個CDN清單。 另請參閱 [多CDN支援](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | 否（預設=Akamai） | 範例： Akamai、Level3、Limelight、Comcast |
| `ptcueformat` | M3U8中存在的自訂廣告提示格式名稱。 | 否 | DPISimple、DPIScte35、Elemental、NBC、NFL或Turner |
| `ptfailover` | 代表資訊清單伺服器識別主要播放清單中指定的主要和容錯移轉資料流，並將它們視為分離集。 這有助於容錯移轉並防止計時錯誤。 (僅適用於Apple HLS裝置)。 另請參閱  [促進HLS播放器切換](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | 否 | true |
| `ptmulticall` | 若設為true，則會對FER發出多個自動廣告呼叫；每個廣告插播各一個。 如果不存在或設為false，則會發出一個廣告呼叫來稽核FER。 | 否 | 布林值 <br> **注意**：下列需求： <ul><li>`ptcueformat` 引數必須設定為nbc</li><li>pttimeline引數會被忽略。</li></ul> |
| `ptplayer` | 發出要求的播放器。 | iOS/Safari | ios-mobileweb |
| `ptrendition` | 由廣告插入自動產生，並由Akamai使用。 請勿新增或移除。 | Akamai廣告縮放器 |  |
| `pttagds` | 啟用 [EXT-X — 不連續 — 序列](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) 標籤 | 否 | true — 資訊清單伺服器在其傳送的每個m3u8檔案中的內容之前都包含一個序列標籤；如果引數不存在或不為true，則資訊清單伺服器不會包含序列標籤。 |
| `pttimeline` | 字串，其中包含廣告投放和內容的所需時間軸，可覆寫內容串流中的廣告插播。 | 否 | [VOD時間表](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | 啟用TS區段授權權杖。<br> **注意**：僅支援Akamai CDN Token | 對於TS區段授權Token | 布林值 |
| `pttrackingmode` | 啟用廣告追蹤；自訂使用者端（簡單）、伺服器端(sstm)或混合(simplesstm)。 | 否 | simple、sstm或simplesstm。<br> **注意**：如果未包含此引數，#EX-X-MARKER會插入資訊清單中。 另請參閱 [EXT-X-MARKER指令](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | 指示資訊清單伺服器僅傳回廣告追蹤資訊。 請勿在啟動程式要求中指定此引數。 | 使用者端追蹤 | 英數字元注意：資訊清單伺服器會忽略所有通過的值。 不過，如果您傳遞null或空字串，資訊清單伺服器會傳回M3U8，而非追蹤資訊。 |
| `pttrackingversion` | 使用者端追蹤資訊的格式版本。 | 使用者端追蹤 | v1、v2、v3或vmap |
| `scteTracking` | 先擷取M3U8 ，然後才能在JSON V2側欄中擷取SCTE追蹤資訊。 <br>此引數會向資訊清單伺服器指出，擷取M3U8的播放器需要擷取SCTE標籤資訊。 | 否（預設： false） | true或false。 <br> **注意**：SCTE-35資料會在JSON側欄中傳回，且具有下列查詢引數值組合： <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | 來自即時點的區段數使用設定前段位移： `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**注意**：僅限即時/線性 | 否（預設： 3.0） | 浮點數 |
| `vebufferLength` | 從即時點開始的秒數。 **注意**：僅限即時/線性。 | 否（預設： 3.0） | 浮點數 |
