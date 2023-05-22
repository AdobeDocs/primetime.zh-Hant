---
title: 詳細記錄
description: 詳細記錄
copied-description: true
exl-id: f2d1b0c2-ba28-4fba-9a4e-71d1421f37fe
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---

# 詳細記錄 {#verbose-logging}

## ptdebug/logging事件說明 {#ptdebug-logging-events}

在啟動清單伺服器會話的調試日誌記錄時，可以添加 `ptdebug` 請求URL的參數，以指定清單伺服器在HTTP標頭中返回的資訊的以下選項：

* `ptdebug=true`
除TRACE_HTTP_HEADER和TRACE_AD_CALL記錄中的大多數調用/響應資料之外的所有記錄。

* `ptdebug=AdCall`
僅TRACE_AD_類型(例如TRACE_AD_CALL)記錄。

* `ptdebug=Header`
僅TRACE_HTTP_HEADER記錄。

## 日誌記錄的格式 {#log-record-formats}

每個日誌記錄都有一個類型和一組欄位，其中有些欄位可能是可選的。 記錄類型之前的所有記錄的欄位相同。 它們提供有關會話的時間戳和資訊。 記錄類型標識記錄的事件類型，後續欄位提供有關記錄事件的資訊。

日誌記錄的結構如下：

`datetime request_id session_id zone_id record_type other fields`.

| 欄位 | 類型 | 說明 |
|---|---|---|
| 日期 | 字串 | 時間戳 |
| 請求ID | 字串 | 清單伺服器使用的請求ID（Unix時間戳） |
| 會話ID | 字串 | 清單伺服器使用的會話ID |
| 區域ID | 整數 | 區域 |
| 記錄類型 | 字串 | 正在記錄的事件類型 |
| 其他欄位 | 不同 | 取決於事件類型 |

此類型的記錄記錄HTTP請求的結果。 超出的欄位 `TRACE_REQUEST_INFO` 按表格中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| 請求方法 | 字串 | HTTP方法(GET或POST) |
| 請求_uri | 字串 | HTTP請求URI（無主機） |
| 請求長度 | 整數 | 請求長度（位元組） |
| 響應長度 | 整數 | 響應長度（位元組） |
| 三角 | 整數 | 處理請求的時間（毫秒） |
| 模組類型 | 字串 | 變型、流或VOD |
| 遠程_地址_aud_client_ip | 字串 | **‡** |
| remote_address_x_fwd_for_hdr_key | 字串 | **‡** |
| 遠程主機埠 | 字串 | **‡** |

**?** 最後三個欄位是可選的。

**一個例子**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER記錄 {#trace-http-header-records}

在清單伺服器和客戶端、廣告伺服器或內容伺服器之間的HTTP調用期間交換的此類型日誌HTTP標頭的記錄。 TRACE_HTTP_HEADER之外的欄位按表中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 請求類型 | 字串 | 請求類型（主或未知） |
| 請求響應 | 字串 | 響應標頭（請求或響應） |
| 標題名稱 | 字串 | HTTP標頭名稱 |
| 標頭_值 | 字串 | Base64編碼的HTTP標頭值 |

>[!NOTE]
>
>的 `request_type` 和 `header_value` 欄位是可選的。

**一個例子**

```shell
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_MISC Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST Cookie aGRu. . .
2015-03-25T06:10:00.928Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST User-Agent TW96aW. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Server bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Content-Type YXBwb. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Last-Modified V2VkL. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE ETag IjIyY2. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Vary QWNjZXB. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Cache-Control bWF4LW. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Expires V2VkL. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Date V2VkLCA. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Age MQ==
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Via MS4xIH. . .
```

### TRACE_AD_CALL記錄 {#tracing-ad-call-records}

此類型的記錄記錄清單伺服器和請求的結果。 超出的欄位 `TRACE_AD_CALL` 按表格中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| 請求持續時間 | 整數 | 從請求到響應的時間（毫秒） |
| ad_server_query_url | 字串 | 廣告調用的URL，包括查詢參數 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器響應（如果未指定，則為Audity） |
| 可用ID | 字串 | 從內容清單檔案中的廣告提示獲得的可用ID（N/A用於VOD） |
| 可用持續時間 | 數 | 可用的持續時間（秒），來自內容清單檔案中的廣告提示（N/A用於VOD） |
| ad_server_response | 字串 | 來自ad伺服器的Base64編碼響應 |

例如：

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT、TRACE_AD_RESOLVE和TRACE_AD_REDIRECT記錄 {#trace-ad-insert-resolve-redirect}

此類型的記錄記錄記錄類型所指示的廣告請求的結果。 記錄類型以外的欄位按表中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 返回HTTP狀態代碼。 |
| 可用ID | 字串 | 可用的ID，來自內容清單檔案（即時）中的廣告提示或來自清單伺服器(VOD)。 |
| ad_type | 字串 | 廣告類型（直接或重定向）。 |
| ad_duration | 整數 | 來自廣告伺服器響應的廣告持續時間（秒）。 |
| ad_content_url | 字串 | 廣告的清單檔案的URL，來自廣告伺服器響應。 |
| **†** ad_content_url_actual | 字串 | 插入廣告的清單檔案的URL。 TRACE_AD_REDIRECT為空。 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器響應（如果未指定，則為警戒）。 |
| ad_id | 字串 | 來自廣告伺服器響應的廣告ID。 |
| creative_id | 字串 | 創作者的ID，來自廣告節點，來自廣告伺服器響應。 |
| **†** ad_call_id | 字串 | 未使用。 保留供將來使用。 |
| 三角 | 整數 | 此事件所花費的時間（毫秒）。 |
| **†** 雜項 | 字串 | 跳過原因廣告。 |

**†** `ad_content_url_actual`。 `ad_call_id`, `misc` 欄位是可選的。

>[!NOTE]
>
>對於 `TRACE_AD_RESOLVE` 和 `TRACE_AD_INSERT`，則 `ad_content_url_actual` 欄位用於已轉碼ad（如果可用）。 否則，該欄位為空 `TRACE_AD_RESOLVE` 或 `ad_content_url` 為 `TRACE_AD_INSERT`。

例如：

```shell
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

<!-- ### TRACE_TRACKING_URL records {#trace-tracking-url-records}

Records of this type log the results of manifest server ad requests. Fields beyond `TRACE_TRACKING_URL` appear in the order shown in the table, separated by tabs.

| Field | Type | Description |
|---|---|---|
| pts | number | Program timestamp. Time within video to call the URL. |
| ad_system | string | Ad system (auditude or freewheel) |
| url | string | URL pinged |
| status | string | HTTP status returned from the ping |

```shell
2015-06-04T23:24:42.000-0700 1426742736208 3086f5cd . . . 12345 TRACE_TRACKING_URL 0.000000 ExampleSystem https://localhost/index.php?stream:test#8.1433485415; sid:3086f5cd . . .;pts:0 200
```

-->

### TRACE轉碼_NO_MEDIA_TO_TRANSCODE記錄 {#trace-transcoding-no-media-to-transcode}

此類記錄記錄缺少廣告創意。 唯一超出的欄位 `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` 的子菜單。

| 欄位 | 類型 | 說明 |
|---|---|---|
| ad_id | 字串 | 完全限定的AD(FQ_AD_ID):Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID:協定:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \]協定：巨幅) |

此類型的記錄記錄清單伺服器發送到CRS的轉碼請求的結果。 超出的欄位 `TRACE_TRANSCODING_REQUESTED` 按表格中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| ad_id | 字串 | 完全限定廣告ID |
| ad_manifest_url | 字串 | 廣告的清單檔案的URL，來自廣告伺服器響應 |
| creative_type | 字串 | 介質類型 |
| 標誌 | 字串 | ID3指示轉碼請求是否包括添加ID3標籤的請求 |
| 目標持續時間 | 字串 | 轉碼創作的目標持續時間（秒） |

此類型的記錄表示請求執行伺服器端跟蹤。 超出的欄位 `TRACE_TRACKING_REQUEST` 按表格中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 跟蹤_url_計數 | 整數 | 跟蹤URL數 |
| 開始 | 浮 | PTS片段開始時間（秒，毫秒精度） |
| 端 | 浮 | PTS片段結束時間（秒，毫秒精度） |

此類型的記錄提供用於伺服器端跟蹤的跟蹤URL。 超出的欄位 `TRACE_TRACKING_REQUEST_URL` 按表格中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 時間戳 | 浮 | 播放會話中ping跟蹤URL的時間（秒，精度為。001）。 |
| ad_system | 字串 | 廣告系統（例如，審級） |
| url | 字串 | 要ping的URL |

此類型的日誌記錄請求清單伺服器為 `WEBVTT` 標題。 超出的欄位 `TRACE_WEBVTT_REQUEST` 按表格中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| vtt_uri | 字串 | 請求的URL |
| 開始 | 浮 | 分割開始時間（秒，毫秒精度） |
| 端 | 浮 | 拆分結束時間（秒，毫秒精度） |

此類型的記錄日誌響應清單伺服器發送給客戶端的 `answer` 請求 `WEBVTT` 標題。 超出的欄位 `TRACE_WEBVTT_RESPONSE` 按表格中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| 響應 | 字串 | 已將Base64編碼的響應發送給客戶端 |

此類型的記錄記錄對清單伺服器發出的請求的日誌響應 `WEBVTT` 標題。 超出的欄位 `TRACE_WEBVTT_SOURCE` 按表格中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| 源 | 字串 | Base64編碼的原始VTT內容 |

此類記錄使清單伺服器能夠記錄在接收廣告時未計畫的事件和資訊。 外面的場 `TRACE_MISC` 包含消息字串。 可能出現的消息包括：

* 已忽略廣告：AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb。。。.m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= seconds, ignore= ignore, redirectAd= redirectAd, priority= priority
* 廣告放置返回空值。
* 廣告成功縫製。
* 廣告調用失敗：錯誤消息。
* 添加User-Agent以獲取原始清單：用戶代理。
* 添加cookie以獲取原始清單：#
* 請求的URL錯誤錯誤消息。 （無法分析變型URL）
* 調用的URL:URL獲得返回：響應代碼。 （即時URL）
* 調用的URL:URL返回代碼：響應代碼。 (VOD URL)
* 解決廣告時發現衝突：中輥起動或中輥端之一位於中輥(VOD)中包含的預輥或預輥內。
* 檢測到URI的處理程式引發的未處理的異常：請求URL。
* 生成變型清單已完成。 （變型）
* 生成變型清單已完成。
* 處理VAST重定向*重定向URL時出現異常*錯誤：錯誤消息。
* 無法獲取廣告清單URL的廣告播放清單。
* 未能生成目標清單。 (HLSManifestResolver)
* 無法分析第一個廣告呼叫響應：錯誤消息。
* 無法處理*GET|POST*路徑請求：請求URL。 （即時/視頻點播）
* 無法處理即時清單請求：請求URL。 （即時）
* 無法返回變型清單：錯誤消息。
* 無法驗證組ID:組ID。
* 正在獲取原始清單：內容URL。 （即時）
* 遵循VAST重定向：重定向URL。
* 找到空的可用。 (VOD)
* 找到 *數* 廣告。 (VOD)
* 收到HTTP請求。 （第一條消息）
* 忽略ad，因為ad響應持續時間（*ad響應持續時間*秒）和實際廣告持續時間（*實際持續時間*秒）之間的差值大於限制。 (HLSManifestResolver)
* 忽略未提供ID值的可用。 (GroupAdResolver.java)
* 忽略提供無效時間值的可用：*availId的時間*=可用ID。
* 忽略提供無效持續時間值的可用：*vailId的持續時間*=可用ID。
* 初始化新會話。 （變型）
* HTTP方法無效。 一定是GET。 (VOD)
* HTTP方法無效。 跟蹤請求必須是GET。 （即時）
* 請求的URL錯誤消息無效。 （變型）
* 組無效。 (HLSManifestResolver)
* 請求無效。 標題不是有效的跟蹤請求。 (VOD)
* 請求無效。 必須在會話建立後發出標題請求。 (VOD)
* 請求無效。 必須在會話建立後發出跟蹤請求。 (VOD)
* 重載組ID的伺服器實例無效：組ID。 （即時）
* 已達到VAST重定向的限制 — 數。
* 進行廣告呼叫：廣告呼叫URL。
* 未找到以下項的清單：內容URL。 （即時）
* 找不到可用ID的匹配可用：可用ID。 (HLSManifestResolver)
* 未找到回放會話。 (HLSManifestResolver)
* 正在處理清單內容URL的VOD請求。
* 正在處理變型。
* 正在處理清單內容URL的標題請求。
* 正在處理跟蹤請求。 (VOD)
* 重定向廣告響應為空。 (VASTStAX)
* 請求：URL。
* 返回GET請求的錯誤響應，因為未找到回放會話。 (VOD)
* 由於內部伺服器錯誤，正在為GET請求返回錯誤響應。
* 為指定無效資產的GET請求返回錯誤響應：廣告請求ID。 (VOD)
* 為指定無效或空組ID的GET請求返回錯誤響應：組ID。 (VOD)
* 為指定無效跟蹤位置值的GET請求返回錯誤響應。 (VOD)
* 返回語法無效的GET請求錯誤響應 — 請求URL。 （即時/視頻點播）
* 使用不支援的HTTP方法返回請求的錯誤響應：GET|POST。 （即時/視頻點播）
* 正在從快取返回清單。 (VOD)
* 伺服器已過載。 無需廣告縫合請求即可繼續。 （變型）
* 開始生成目標清單。 (HLSManifestResolver)
* 開始從以下位置生成變型清單：內容URL。 （變型）
* 開始將廣告拼接到清單中。 (VODHLSResolver)
* 試圖在 `HH:MM:SS`:AdPlacement \[adManifestURL= ad Manifest URL, durationSeconds= seconds, ignore= ignore, redirectAd= redirect ad, priority= priority。\] \(HLSManifestResolver\)
* 由於時間軸無效，無法獲取廣告 — 返回沒有廣告的內容。 (VOD)
* 無法獲取廣告 — 返回沒有廣告的內容。 (VOD)
* 無法獲取廣告查詢，未提供內容URL。 (VOD)
* 收到有效的URL。 （VOD/變型）
* 找不到變型M3U8。 （變型）

### TRACE_回放_進度記錄 {#trace-playback-progress-records}

清單伺服器在伺服器端跟蹤工作流期間接收關於回放進度的信號時生成這種記錄。 超出的欄位 `TRACE_PLAYBACK_PROGRESS` 按表格中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | HTTP狀態代碼 |
| 頻寬 | 整數 | 流的頻寬 |
| 點 | 整數 | 流內的PTS時間 |
| ms_time | 整數 | 清單伺服器生成跟蹤URL的時間 |
| url | 字串 | 重定向URL |
| **。** 標頭_用戶_代理 | 字串 | HTTP用戶代理標頭 |
| **。** 標頭_dnt | 整數 | HTTP不跟蹤標頭 |
| **。** 有效_remote_address | 字串 | IPv4有效遠程地址 |
| **。** 遠程地址 | 字串 | IPv4遠程地址 |

**。** 最後四個欄位是可選的。

## 多比特率流 {#multiple-bitrate-streams}

客戶端廣告插入請求通常在變型M3U8格式的播放清單中指定一個以上的比特率。 清單伺服器生成並返回新的變型M3U8檔案，該新變型M3U8檔案包含針對每個比特率的單獨M3U8鏈路。 它還生成一個唯一的組ID來將這些M3U8連接在一起。

清單伺服器使用客戶端的BootstrapURL請求中的資訊來檢索內容變體播放清單。 它生成一個新的變型播放清單，該播放清單包含到流級內容的清單伺服器連結。 客戶端使用它們構造和插入請求。 清單伺服器的流級內容連結具有以下格式：

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **即時/視頻點播**
清單伺服器根據內容的播放清單類型設定此值：即時/線性(
`#EXT-X-PLAYLIST-TYPE:EVENT`)或VOD(`#EXT-X-PLAYLIST-TYPE:VOD`)

* **publisherAssetID**
Publisher針對BootstrapURL請求中提供的特定內容的唯一ID。

* **格式**
清單伺服器根據 
`BANDWIDTH` 內容流的值，並使用它將廣告的比特率與內容的比特率匹配。 除非具有最低比特率的廣告格式副本超過內容的比特率，否則廣告比特率不能超過內容的比特率。

* **組ID**
清單伺服器生成此值，並使用它來確保它始終如一地放置廣告，而不管客戶請求廣告的格式副本為什麼。

* **比特率流的base64編碼URL**
清單伺服器URL安全base64對內容流的絕對URL進行編碼。 每個流都有其自己的URL。

* **查詢參數**
在BootstrapURL請求中提供的查詢參數。
