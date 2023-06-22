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

## ptdebug/記錄事件說明 {#ptdebug-logging-events}

為資訊清單伺服器工作階段起始偵錯記錄時，您可以新增 `ptdebug` 要求URL的引數，指定資訊清單伺服器傳回HTTP標頭之資訊的下列選項：

* `ptdebug=true`
除了TRACE_HTTP_HEADER和來自TRACE_AD_CALL記錄的大部分呼叫/回應資料以外的所有記錄。

* `ptdebug=AdCall`
僅限TRACE_AD_型別(例如TRACE_AD_CALL)記錄。

* `ptdebug=Header`
僅限TRACE_HTTP_HEADER記錄。

## 記錄檔記錄格式 {#log-record-formats}

每個記錄檔記錄都有一個型別和一組欄位，其中一些可能是選擇性的。 記錄型別之前的所有記錄的欄位都是相同的。 它們會提供工作階段的時間戳記和資訊。 記錄型別會識別所記錄的事件的型別，而後續欄位會提供有關所記錄事件的資訊。

記錄檔記錄的結構如下：

`datetime request_id session_id zone_id record_type other fields`.

| 欄位 | 型別 | 說明 |
|---|---|---|
| 日期時間 | 字串 | 時間戳記 |
| request_id | 字串 | 資訊清單伺服器使用的請求ID （Unix時間戳記） |
| session_id | 字串 | 資訊清單伺服器使用的工作階段ID |
| zone_id | 整數 | 區域 |
| record_type | 字串 | 所記錄的事件的型別 |
| 其他欄位 | 不盡相同 | 視事件型別而定 |

此型別的記錄會記錄HTTP請求的結果。 欄位超出 `TRACE_REQUEST_INFO` 會以表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| request_method | 字串 | HTTP方法(GET或POST) |
| request_uri | 字串 | HTTP要求URI （不含主機） |
| request_length | 整數 | 要求長度（位元） |
| response_length | 整數 | 回應長度（位元） |
| delta | 整數 | 處理要求的時間（毫秒） |
| 模組型別 | 字串 | 變體、資料流或VOD |
| remote_address_aud_client_ip | 字串 | **‡** |
| remote_address_x_fwd_for_hdr_key | 字串 | **‡** |
| remote_host_port | 字串 | **‡** |

**‡** 最後三個欄位是選用欄位。

**範例**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER記錄 {#trace-http-header-records}

此型別的記錄會記錄資訊清單伺服器與使用者端、廣告伺服器或內容伺服器之間的HTTP呼叫期間交換的HTTP標頭。 TRACE_HTTP_HEADER以外的欄位會依表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| request_type | 字串 | 請求型別（主要或未知） |
| request_response | 字串 | 回應標頭（請求或回應） |
| header_name | 字串 | HTTP標頭名稱 |
| header_值 | 字串 | Base64編碼的HTTP標頭值 |

>[!NOTE]
>
>此 `request_type` 和 `header_value` 欄位為選用。

**範例**

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

此型別的記錄記錄會記錄資訊清單伺服器和要求的結果。 欄位超出 `TRACE_AD_CALL` 會以表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| request_duration | 整數 | 從要求到回應的時間（毫秒） |
| ad_server_query_url | 字串 | 廣告呼叫的URL，包括查詢引數 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器回應（若未指定，則為稽核） |
| avail_id | 字串 | 從內容資訊清單檔案中的廣告提示取得的有效的ID （VOD不適用） |
| avail_duration | 數字 | 從內容資訊清單檔案中的廣告提示取得廣告的持續時間（秒） （VOD不適用） |
| ad_server_response | 字串 | 來自廣告伺服器的Base64編碼回應 |

範例：

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT、TRACE_AD_RESOLVE和TRACE_AD_REDIRECT記錄 {#trace-ad-insert-resolve-redirect}

此型別的記錄會記錄記錄該記錄型別所指示的廣告請求的結果。 記錄型別以外的欄位會以表格中顯示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回HTTP狀態代碼。 |
| avail_id | 字串 | 從內容資訊清單檔案（即時）中的廣告提示或來自資訊清單伺服器(VOD)的可用的ID。 |
| ad_type | 字串 | 廣告型別（直接或重新導向）。 |
| ad_duration | 整數 | 來自廣告伺服器回應的廣告持續時間（秒）。 |
| ad_content_url | 字串 | 廣告資訊清單檔案的URL，來自廣告伺服器回應。 |
| **†** ad_content_url_actual | 字串 | 插入廣告資訊清單檔案的URL。 留空表示TRACE_AD_REDIRECT。 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器回應（若未指定，則為Auditude）。 |
| ad_id | 字串 | 廣告ID，來自廣告伺服器回應。 |
| creative_id | 字串 | 廣告節點和廣告伺服器回應中的創意ID。 |
| **†** ad_call_id | 字串 | 未使用。 保留以供日後使用。 |
| delta | 整數 | 此事件花費的時間（毫秒）。 |
| **†** 雜項 | 字串 | 略過廣告的原因。 |

**†** `ad_content_url_actual`， `ad_call_id`、和 `misc` 欄位為選用。

>[!NOTE]
>
>對象 `TRACE_AD_RESOLVE` 和 `TRACE_AD_INSERT`，此網址位於 `ad_content_url_actual` 欄位適用於轉碼廣告（若有）。 否則欄位會空白 `TRACE_AD_RESOLVE` 或與 `ad_content_url` 的 `TRACE_AD_INSERT`.

範例：

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

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE記錄 {#trace-transcoding-no-media-to-transcode}

此型別的記錄會記錄缺少的廣告創意。 唯一超出的欄位 `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` 會顯示在表格中。

| 欄位 | 型別 | 說明 |
|---|---|---|
| ad_id | 字串 | 完整廣告識別碼(FQ_AD_ID： Q_AD_ID\[；Q_AD_ID\[；Q_AD_ID...\] \] Q_AD_ID：通訊協定:AD_SYSTEM:AD_ID\[：CREATIVE_ID\[：MEDIA_ID\] \]通訊協定： AUDITUDE，VAST) |

此型別的記錄會記錄資訊清單伺服器傳送至CRS的轉碼請求結果。 欄位超出 `TRACE_TRANSCODING_REQUESTED` 會以表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| ad_id | 字串 | 完整廣告ID |
| ad_manifest_url | 字串 | 廣告資訊清單檔案的URL，來自廣告伺服器回應 |
| creative_type | 字串 | 媒體型別 |
| 標幟 | 字串 | ID3指出轉碼請求是否包含新增ID3標籤的請求 |
| target_duration | 字串 | 轉碼創意的目標持續時間（秒） |

此型別的記錄表示執行伺服器端追蹤的請求。 欄位超出 `TRACE_TRACKING_REQUEST` 會以表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| tracking_url_count | 整數 | 追蹤URL |
| 開始 | 浮點數 | PTS片段開始時間（以毫秒為精確度計算，以秒為單位） |
| 結束 | 浮點數 | PTS片段結束時間（以毫秒為精確度計算，以秒為單位） |

此型別的記錄會提供伺服器端追蹤的追蹤URL。 欄位超出 `TRACE_TRACKING_REQUEST_URL` 會以表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| timestamp | 浮點數 | 在播放工作階段內偵測追蹤URL所需的時間（秒，精確度為。001）。 |
| ad_system | 字串 | 廣告系統（例如auditude） |
| url | 字串 | 要偵測的URL |

資訊清單伺服器針對此型別的記錄要求 `WEBVTT` 註解。 欄位超出 `TRACE_WEBVTT_REQUEST` 會以表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| vtt_uri | 字串 | 請求的URL |
| 開始 | 浮點數 | 分割開始時間（以毫秒精確度計算，以秒為單位） |
| 結束 | 浮點數 | 分割結束時間（以毫秒精確度計算，以秒為單位） |

資訊清單伺服器傳送至使用者端的此型別記錄檔回應記錄位於 `answer` 至以下專案的請求 `WEBVTT` 註解。 欄位超出 `TRACE_WEBVTT_RESPONSE` 會以表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| 回應 | 字串 | 傳送至使用者端的Base64編碼回應 |

此型別的記錄會回應資訊清單伺服器的要求 `WEBVTT` 註解。 欄位超出 `TRACE_WEBVTT_SOURCE` 會以表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| source | 字串 | Base64編碼原始VTT內容 |

此型別的記錄可讓資訊清單伺服器記錄事件和資訊，而這些資訊不是為擷取廣告而計畫的。 超出欄位 `TRACE_MISC` 由訊息字串組成。 可能顯示的訊息包括：

* 已忽略廣告： AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb。...m3u8， durationSeconds=15.0， ignore=false， redirectAd=false， priority=1\]
* AdPlacement adManifestURL= adManifestURL， durationSeconds=秒， ignore= ignore， redirectAd= redirectAd， priority= priority
* 廣告放置傳回null。
* 廣告已成功拼接。
* 廣告呼叫失敗：錯誤訊息。
* 正在新增使用者代理程式以擷取原始資訊清單：使用者代理。
* 新增Cookie以擷取原始資訊清單： #
* 錯誤的URL請求的URL錯誤訊息。 （無法剖析變體URL）
* 已呼叫URL： URL已傳回：回應代碼。 （即時URL）
* 已呼叫URL： URL傳回碼：回應碼。 ( VOD URL)
* 解決廣告時發現衝突：其中一個 — 中段開始或中段結束落在中段(VOD)中包含的前段或前段。
* 偵測到URI：要求URL的處理常式擲回未處理的例外狀況。
* 完成產生變體資訊清單。 （變體）
* 完成產生變體資訊清單。
* 處理VAST重新導向*重新導向URL *錯誤：錯誤訊息時發生例外狀況。
* 無法擷取廣告資訊清單URL的廣告播放清單。
* 無法產生目標資訊清單。 (HLSManifestResolver)
* 無法剖析第一個廣告呼叫回應：錯誤訊息。
* 無法處理以下路徑的*GET|POST*要求：要求URL。 （即時/VOD）
* 無法處理即時資訊清單要求：要求URL。 （即時）
* 無法傳回變體資訊清單：錯誤訊息。
* 無法驗證群組識別碼：群組識別碼。
* 正在擷取原始資訊清單：內容URL。 （即時）
* 下列VAST重新導向：重新導向URL。
* 找到空的可用性。 (VOD)
* 已找到 *數字* 廣告。 (VOD)
* 已收到HTTP要求。 （第一則訊息）
* 略過廣告，因為廣告回應持續時間（*廣告回應持續時間*秒）與實際廣告持續時間（*實際持續時間*秒）之間的差異大於限制。 (HLSManifestResolver)
* 忽略未提供ID值的可用性。 (GroupAdResolver.java)
* 忽略提供無效時間值的可用性： *time *for availId = avail ID。
* 忽略提供無效持續時間值的可用性： *duration *for availId = avail ID。
* 初始化新工作階段。 （變體）
* 無效的HTTP方法。 它必須是GET。 (VOD)
* 無效的HTTP方法。 追蹤要求必須是GET。 （即時）
* 無效的URL請求的URL錯誤訊息。 （變體）
* 無效的群組。 (HLSManifestResolver)
* 無效的請求。 註解不是有效的追蹤要求。 (VOD)
* 無效的請求。 註解請求必須在工作階段建立後發出。 (VOD)
* 無效的請求。 追蹤要求必須在工作階段建立後提出。 (VOD)
* 多載群組識別碼的伺服器執行個體無效：群組識別碼。 （即時）
* 已達到VAST重新導向的限制 — 數字。
* 進行廣告呼叫：廣告呼叫URL。
* 找不到：內容URL的資訊清單。 （即時）
* 找不到相符的可用性ID：可用性ID。 (HLSManifestResolver)
* 找不到播放工作階段。 (HLSManifestResolver)
* 正在處理資訊清單內容URL的VOD請求。
* 正在處理變體。
* 正在處理資訊清單內容URL的標題要求。
* 正在處理追蹤要求。 (VOD)
* 重新導向廣告回應為空白。 ( VASTStAX)
* 請求： URL。
* 傳回GET要求的錯誤回應，因為找不到播放工作階段。 (VOD)
* 因內部伺服器錯誤而傳回GET要求的錯誤回應。
* 針對指定無效資產的GET請求傳回錯誤回應：廣告請求ID。 (VOD)
* 針對指定無效或空白群組ID的GET要求傳回錯誤回應：群組ID。 (VOD)
* 針對指定無效追蹤位置值的GET要求傳回錯誤回應。 (VOD)
* 使用無效語法傳回GET請求的錯誤回應 — 請求URL。 （即時/VOD）
* 使用不支援的HTTP方法傳回要求的錯誤回應：GET|POST。 （即時/VOD）
* 正在從快取傳回資訊清單。 (VOD)
* 伺服器超載。 繼續進行而不需廣告拼接請求。 （變體）
* 開始產生目標資訊清單。 (HLSManifestResolver)
* 開始從下列來源產生變體資訊清單：內容URL。 （變體）
* 開始將廣告拼接至資訊清單。 (VODHLSResolver)
* 嘗試拼接廣告 `HH:MM:SS`： AdPlacement \[adManifestURL=廣告資訊清單URL， durationSeconds=秒， ignore=忽略， redirectAd=重新導向廣告， priority=優先順序。\] \(HLSManifestResolver\)
* 因為無效的時間軸而無法取得廣告 — 傳回了沒有廣告的內容。 (VOD)
* 無法取得廣告 — 傳回不含廣告的內容。 (VOD)
* 無法取得廣告查詢，且未提供內容URL。 (VOD)
* 收到有效的URL。 （VOD/變體）
* 找不到變體M3U8。 （變體）

### TRACE_播放_進度記錄 {#trace-playback-progress-records}

資訊清單伺服器會在伺服器端追蹤工作流程期間收到有關播放進度的訊號時，產生此類記錄。 欄位超出 `TRACE_PLAYBACK_PROGRESS` 會以表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|---|---|---|
| 狀態 | 字串 | HTTP狀態代碼 |
| 頻寬 | 整數 | 串流的頻寬 |
| 分 | 整數 | 串流中的PTS時間 |
| ms_time | 整數 | 資訊清單伺服器產生追蹤URL的時間 |
| url | 字串 | 重新導向URL |
| **？** header_user_agent | 字串 | HTTP User-Agent標頭 |
| **？** header_dnt | 整數 | HTTP do-not-track標頭 |
| **？** effective_remote_address | 字串 | IPv4有效的遠端位址 |
| **？** remote_address | 字串 | Ipv4遠端位址 |

**？** 最後四個欄位是選用欄位。

## 多位元速率資料流 {#multiple-bitrate-streams}

廣告插入的使用者端請求通常會在變體M3U8格式的播放清單中指定超過一個位元速率。 資訊清單伺服器會產生並傳回新的變體M3U8檔案，其中包含每個位元速率的個別M3U8連結。 它也會產生唯一的群組ID，以將這些M3U8繫結在一起。

資訊清單伺服器會使用使用者端BootstrapURL請求中的資訊來擷取內容變體播放清單。 它會產生包含資料流層級內容之資訊清單伺服器連結的新變體播放清單。 使用者端會使用這些來建構廣告插入請求。 資訊清單伺服器的串流層級內容連結格式如下：

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/vod**
資訊清單伺服器會根據內容的播放清單型別設定此值：即時/線性(
`#EXT-X-PLAYLIST-TYPE:EVENT`)或VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* **publisherAssetId**
Publisher在BootstrapURL要求中提供之特定內容的唯一ID。

* **轉譯**
資訊清單伺服器會根據 
`BANDWIDTH` 內容串流的值，並使用它來比對廣告的位元速率與內容的位元速率。 廣告位元速率不能超過內容的位元速率，除非具有最低位元速率的廣告轉譯超過此速率。

* **groupID**
資訊清單伺服器會產生此值，並使用它來確保無論使用者端要求廣告的位元速率轉譯，都能一致地放置廣告。

* **位元速率資料流的base64編碼url**
資訊清單伺服器URL安全的base64會編碼內容資料流的絕對URL。 每個資料流都有自己的URL。

* **查詢引數**
BootstrapURL要求中提供的查詢引數。
