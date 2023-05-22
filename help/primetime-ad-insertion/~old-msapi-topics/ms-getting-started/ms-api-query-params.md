---
title: 清單伺服器查詢參數
description: 查詢參數告訴清單伺服器客戶端發送請求的類型以及該客戶端希望清單伺服器執行的操作。 有些是必需的，有些則具有特定的可接受格式或值。
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# 清單伺服器查詢參數 {#ms-query-params}

查詢參數告訴清單伺服器客戶端發送請求的類型以及該客戶端希望清單伺服器執行的操作。 有些是必需的，有些則具有特定的可接受格式或值。

完整URL由基URL和問號組成，然後 `parameterName=value` 參數，用符號分隔： `Base URL?name1=value1&name2=value2& . . .&name n=value n`。

## 已識別的參數 {#section_072845B7FA94468C8068E9092983C9E6}

清單伺服器識別以下參數。 它處理它們或將它們連同所有無法識別的參數一起傳遞給廣告伺服器。

| 鍵 | 說明 | 必需 | 有效值 |
|---|---|---|---|
| `__sid__` | 清單伺服器用於生成會話ID的唯一ID。 | 是 | 字母數字 |
| g | 客戶端設備類型 | 當目標規則依賴於設備類型時 | 請參閱清單位置 [客戶端類型](https://adobeprimetime.zendesk.com)。 需要Zendesk訪問。 |
| k | 自定義廣告目標的關鍵字 | 否 | 格式為URL安全字串 `key1=value1;key2=value2;. . .` |
| 烏 | 黃金時段廣告插入資產ID。 | 是 | MD5哈希值 |
| z | 資產的黃金時段廣告插入區域ID。 | 是 | 整數 |
| enableC3 | 客戶端位於C3窗口中。 如果為true，則僅替換本地可用；否則，替換所有可用。 | 否 | 布爾型 |
| 活 | 指示內容是Live還是VOD（視頻點播）流。 | Akamai Ad Scaler或iOSSafari客戶。 | 布爾型 |
| `pabimode` | [啟用部分廣告分段插入](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) 支援。 <br> 如果為true或start，則啟用。<br> 如果為false，則禁用。 | 否（預設為禁用） | start 、 true或false |
| `ptadwindow` | 廣告縫合窗口的持續時間（秒）:當DVR用戶加入流時，要回到多遠才能查找廣告。 | 否（預設值= 1800） | 0至1800 |
| `ptassetid` | 發佈者分配和維護的內容的唯一ID。 | 阿卡邁 | URL安全字串 |
| `ptcdn` | 主機轉碼資產的一個或多個CDN的清單。 請參閱 [多CDN支援](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md)。 | 否（預設值=Akamai） | 示例：Akamai、Level3、Velting、Comcast |
| `ptcueformat` | M3U8中存在的自定義廣告提示格式的名稱。 | 否 | DPISimple、DPIScte35、Elemental、NBC、NFL或Turner |
| `ptfailover` | 向清單伺服器發出信號，以標識主播放清單中指定的主流和故障轉移流，並將它們視為不相交集。 這便於故障切換並防止計時錯誤。 (僅限AppleHLS設備)。 請參閱  [促進HLS播放器切換](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md)。 | 否 | 真 |
| `ptmulticall` | 如果設定為true，則會多次向FER發出Auditude廣告；每個廣告時段一個。 如果缺席或設為假，則向FER發出一個廣告。 | 否 | 布爾型 <br> **注釋**:以下要求： <ul><li>`ptcueformat` 參數必須設定為nbc</li><li>將忽略pttimeline參數。</li></ul> |
| `ptplayer` | 播放器發出請求。 | iOS/薩法里 | ios mobileweb |
| `ptrendition` | 通過廣告插入自動生成並由Akamai使用。 不要添加或刪除。 | 阿卡邁 |  |
| `pttagds` | 啟用 [EXT-X — 不連續序列](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) 標籤 | 否 | true — 清單伺服器在其發送的每個m3u8檔案中的內容之前包含序列標籤；如果參數不存在或不為true，則清單伺服器不包括序列標籤。 |
| `pttimeline` | 包含廣告放置和內容所需時間線的字串，該字串覆蓋內容流中的廣告斷點。 | 否 | [VOD時間線](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | 啟用TS段授權令牌。<br> **注釋**:僅支援Akamai CDN令牌 | 對於TS段授權令牌 | 布爾型 |
| `pttrackingmode` | 啟用廣告跟蹤；自定義客戶端(simple)、伺服器端(sstm)或混合(simplesstm)。 | 否 | simple 、 sstm或simplesstm。<br> **注釋**:如果未包括此參數，則#EX-X-MARKER將注入清單。 請參閱 [EXT-X-MARKER指令](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md)。 |
| `pttrackingposition` | 指示清單伺服器僅返回廣告跟蹤資訊。 不要在引導請求中指定此參數。 | 客戶端跟蹤 | 字母數字注釋：清單伺服器忽略所有傳遞的值。 但是，如果傳遞空字串或空字串，則清單伺服器將返回M3U8，而不返回跟蹤資訊。 |
| `pttrackingversion` | 客戶端跟蹤資訊的格式版本。 | 客戶端跟蹤 | v1 、 v2 、 v3或vmap |
| `scteTracking` | 在JSON V2 Sidecar中提取SCTE跟蹤資訊之前，請提取M3U8。 <br>此參數向清單伺服器指示讀取M3U8的播放器需要檢索SCTE標籤資訊。 | 否(預設值：假) | 真或假。 <br> **注釋**:SCTE-35資料在JSONsidecar中返回，並包含以下查詢參數值組合： <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | 從即時點開始的段數預滾偏移配置為： `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**注釋**:僅限Live/Linear | 否(預設值：3.0) | 浮動 |
| `vebufferLength` | 從即時點開始的秒數。 **注釋**:僅限Live/Linear。 | 否(預設值：3.0) | 浮動 |
