---
title: 詳細記錄
description: 詳細記錄
copied-description: true
exl-id: f2d1b0c2-ba28-4fba-9a4e-71d1421f37fe
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 0%

---

# 詳細記錄{#verbose-logging}

## ptdebug/logging事件說明{#ptdebug-logging-events}

在啟動資訊清單伺服器工作階段的除錯記錄時，您可將`ptdebug`參數新增至請求URL，以指定資訊清單伺服器在HTTP標題中傳回的資訊：

* `ptdebug=true`
除TRACE_HTTP_HEADER和TRACE_AD_CALL記錄中的大多數調用／響應資料之外的所有記錄。

* `ptdebug=AdCall`
只有TRACE_AD_type(例如TRACE_AD_CALL)記錄。

* `ptdebug=Header`
僅TRACE_HTTP_HEADER記錄。

## 日誌記錄的格式{#log-record-formats}

每個記錄都有一個類型和一組欄位，其中有些欄位可能是可選的。 直到記錄類型的所有記錄欄位都相同。 它們會提供作業的時間戳記和資訊。 記錄類型可識別記錄的事件類型，而後續欄位則提供記錄事件的相關資訊。

日誌記錄的結構如下：

`datetime request_id session_id zone_id record_type other fields`.

| 欄位 | 類型 | 說明 |
|---|---|---|
| 日期時間 | 字串 | 時間戳記 |
| request_id | 字串 | 資訊清單伺服器使用的請求ID（Unix時間戳記） |
| session_id | 字串 | 資訊清單伺服器使用的工作階段ID |
| zone_id | 整數 | 區域 |
| record_type | 字串 | 記錄的事件類型 |
| 其他欄位 | 差異 | 取決於事件類型 |

此類型的記錄記錄HTTP請求的結果。 `TRACE_REQUEST_INFO`以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| request_method | 字串 | HTTP方法(GET或POST) |
| request_uri | 字串 | HTTP請求URI（無主機） |
| request_length | 整數 | 請求長度（位元組） |
| response_length | 整數 | 回應長度（位元組） |
| δ | 整數 | 處理請求的時間（毫秒） |
| module_type | 字串 | 變體、串流或VOD |
| remote_address_aud_client_ip | 字串 | **‡** |
| remote_address_x_fwd_for_hdr_key | 字串 | **‡** |
| remote_host_port | 字串 | **‡** |

**‡最** 後三個欄位是選用的。

**範例**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER記錄{#trace-http-header-records}

在資訊清單伺服器與用戶端、廣告伺服器或內容伺服器之間進行HTTP呼叫期間交換的此類記錄記錄HTTP標頭。 TRACE_HTTP_HEADER以外的欄位以表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| request_type | 字串 | 請求類型（MAIN或UNKNOWN） |
| request_response | 字串 | 回應標題（請求或回應） |
| header_name | 字串 | HTTP標題名稱 |
| header_value | 字串 | Base64編碼的HTTP標頭值 |

>[!NOTE]
>
>`request_type`和`header_value`欄位為選擇性欄位。

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

### TRACEAD_CALL記錄{#tracing-ad-call-records}

此類型的記錄會記錄資訊清單伺服器和要求的結果。 `TRACE_AD_CALL`以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| request_duration | 整數 | 請求到回應的時間（毫秒） |
| ad_server_query_url | 字串 | 廣告呼叫的URL，包括查詢參數 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器回應（若未指定，則為Auditude） |
| avail_id | 字串 | 可用的ID，來自內容資訊清單檔案中的廣告提示（VOD的N/A） |
| avail_duration | 數字 | 可用的持續時間（秒），來自內容資訊清單檔案中的廣告提示（VOD為N/A） |
| ad_server_response | 字串 | 來自廣告伺服器的Base64編碼回應 |

例如：

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT、TRACE_AD_RESOLVE和TRACE_AD_REDIRECT記錄{#trace-ad-insert-resolve-redirect}

此類型的記錄會記錄記錄類型所指示之廣告請求的結果。 記錄類型以外的欄位按表中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回HTTP狀態代碼。 |
| avail_id | 字串 | 可用的ID，來自內容資訊清單檔案（即時）中的廣告提示，或來自資訊清單伺服器(VOD)。 |
| ad_type | 字串 | 廣告類型（直接或重新導向）。 |
| ad_duration | 整數 | 廣告伺服器回應的廣告持續時間（秒）。 |
| ad_content_url | 字串 | 來自廣告伺服器回應的廣告資訊清單檔案的URL。 |
| **†** ad_content_url_actual | 字串 | 已插入廣告資訊清單檔案的URL。 TRACE_AD_REDIRECT為空。 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器回應（若未指定，則為Auditude）。 |
| ad_id | 字串 | 來自廣告伺服器回應的廣告ID。 |
| creative_id | 字串 | 來自廣告節點、來自廣告伺服器回應的創作者ID。 |
| **†** ad_call_id | 字串 | 未使用。 留待日後使用。 |
| δ | 整數 | 此事件所花費的時間（毫秒）。 |
| **†雜** 項 | 字串 | 廣告跳過的原因。 |

**†、** `ad_content_url_actual`和欄 `ad_call_id`位皆 `misc` 為選用。

>[!NOTE]
>
>對於`TRACE_AD_RESOLVE`和`TRACE_AD_INSERT`,`ad_content_url_actual`欄位中的URL會用於轉碼廣告（如果有的話）。 否則，`TRACE_AD_RESOLVE`的欄位為空，或`TRACE_AD_INSERT`的欄位與`ad_content_url`相同。

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

### TRACE轉碼_RODCING_NO_MEDIA_TO_TRANSCODE記錄{#trace-transcoding-no-media-to-transcode}

此類型的記錄記錄遺失廣告創意。 表格中將顯示`TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE`以外的唯一欄位。

| 欄位 | 類型 | 說明 |
|---|---|---|
| ad_id | 字串 | 完全限定的廣告ID(FQ_AD_ID:Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID:通訊協定：AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \]通訊協定：AUDITUDE, VAST) |

此類型的記錄記錄資訊清單伺服器傳送至CRS的轉碼請求結果。 `TRACE_TRANSCODING_REQUESTED`以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| ad_id | 字串 | 完全限定的廣告ID |
| ad_manifest_url | 字串 | 來自廣告伺服器回應的廣告資訊清單檔案的URL |
| creative_type | 字串 | 媒體類型 |
| 旗標 | 字串 | ID3指出轉碼請求是否包含新增ID3標籤的請求 |
| target_duration | 字串 | 轉碼創意素材的目標持續時間（秒） |

此類型的記錄會指出執行伺服器端追蹤的要求。 `TRACE_TRACKING_REQUEST`以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| tracking_url_count | 整數 | 追蹤URL的數量 |
| start | 浮水 | PTS碎片開始時間（秒，精確到毫秒） |
| end | 浮水 | PTS片段結束時間（秒數，精確到毫秒） |

此類型的記錄提供伺服器端追蹤的追蹤URL。 `TRACE_TRACKING_REQUEST_URL`以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 時間戳記 | 浮水 | 播放工作階段內的時間（秒數，精確度為。001），以ping追蹤URL。 |
| ad_system | 字串 | 廣告系統（例如auditude） |
| url | 字串 | Ping的URL |

此類型記錄會要求資訊清單伺服器為`WEBVTT`標題編寫。 `TRACE_WEBVTT_REQUEST`以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| vtt_uri | 字串 | 請求的URL |
| start | 浮水 | 分割開始時間（秒數，精確到毫秒） |
| end | 浮水 | 分割結束時間（秒數，精確到毫秒） |

此類型的記錄會回應資訊清單伺服器傳送至`answer`客戶端的`WEBVTT`標題要求。 `TRACE_WEBVTT_RESPONSE`以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| 響應 | 字串 | 傳送給用戶端的Base64編碼回應 |

此類型的記錄會記錄對資訊清單伺服器發出`WEBVTT`標題的請求的回應。 `TRACE_WEBVTT_SOURCE`以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| 來源 | 字串 | Base64編碼的原始VTT內容 |

此類型的記錄可讓資訊清單伺服器記錄未計畫在擷取廣告時的事件和資訊。 `TRACE_MISC`以外的欄位包含訊息字串。 可能出現的訊息包括：

* 已忽略廣告：AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb。...m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= seconds, ignore= ignore, redirectAd= redirectAd, priority= priority
* 廣告位置傳回null。
* 成功銜接廣告。
* 廣告呼叫失敗：錯誤訊息。
* 新增User-Agent以擷取原始資訊清單：user-agent。
* 新增Cookie以擷取原始資訊清單：#
* 請求的URL錯誤訊息。 （無法解析變型URL）
* 呼叫的url:URL已傳回：回應碼。 （即時URL）
* 呼叫的url:URL傳回代碼：回應碼。 (VOD URL)
* 解決廣告時發現衝突：其中一個——中間輥開始端或中間輥結束端落在中間輥(VOD)中包含的前輥或前輥內。
* URI的處理程式檢測到未處理的異常：請求URL。
* 已完成變型資訊清單的產生。 （變體）
* 已完成變型資訊清單的產生。
* 處理VAST重新導向*重新導向URL *錯誤：錯誤訊息。
* 無法擷取廣告的廣告清單URL播放清單。
* 無法產生目標資訊清單。 (HLSManifestResolver)
* 無法解析第一個廣告呼叫回應：錯誤訊息。
* 無法處理*GET|POST*路徑請求：請求URL。 （即時/VOD）
* 無法處理即時資訊清單請求：請求URL。 （即時）
* 無法傳回變型資訊清單：錯誤訊息。
* 無法驗證組ID:群組ID。
* 正在擷取原始資訊清單：內容URL。 （即時）
* 遵循廣泛的重新導向：重新導向URL。
* 找到空的可用。 (VOD)
* 找到&#x200B;*number*&#x200B;廣告。 (VOD)
* 收到HTTP請求。 （第一條訊息）
* 忽略廣告，因為廣告回應持續時間（*廣告回應持續時間*秒）與實際廣告持續時間（*實際持續時間*秒）之間的差異大於限制。 (HLSManifestResolver)
* 忽略未提供ID值的可用值。 (GroupAdResolver.java)
* 正在忽略提供無效時間值的可用：*vailId的時間*=可用ID。
* 正在忽略提供無效持續時間值的可用值：*duration *for availId = avail ID.
* 初始化新會話。 （變體）
* 無效的HTTP方法。 一定是GET。 (VOD)
* 無效的HTTP方法。 追蹤要求必須是GET。 （即時）
* 請求的URL錯誤訊息無效。 （變體）
* 無效的組。 (HLSManifestResolver)
* 請求無效。 標題不是有效的追蹤請求。 (VOD)
* 請求無效。 標題請求必須在會話建立後進行。 (VOD)
* 請求無效。 必須在建立工作階段後提出追蹤要求。 (VOD)
* 過載組ID的伺服器實例無效：群組ID。 （即時）
* 已達到VAST重新導向的限制——數目。
* 進行廣告呼叫：廣告呼叫URL。
* 找不到以下項目的清單：內容URL。 （即時）
* 找不到可用ID的匹配可用值：可用ID。 (HLSManifestResolver)
* 找不到播放會話。 (HLSManifestResolver)
* 正在處理資訊清單內容URL的VOD請求。
* 正在處理變型。
* 處理資訊清單內容URL的標題請求。
* 正在處理追蹤請求。 (VOD)
* 重新導向廣告回應空白。 (VASTStAX)
* 請求：URL。
* 傳回GET請求的錯誤回應，因為找不到播放作業。 (VOD)
* 因內部伺服器錯誤而傳回GET要求的錯誤回應。
* 針對指定無效資產的GET請求傳回錯誤回應：廣告請求ID。 (VOD)
* 傳回指定無效或空白群組ID之GET要求的錯誤回應：群組ID。 (VOD)
* 傳回指定無效追蹤位置值之GET要求的錯誤回應。 (VOD)
* 以無效語法傳回GET請求的錯誤回應——請求URL。 （即時/VOD）
* 使用不支援的HTTP方法傳回請求的錯誤回應：GET|POST。 （即時/VOD）
* 從快取傳回資訊清單。 (VOD)
* 伺服器過載。 不需要廣告插圖請求即可繼續。 （變體）
* 開始產生目標資訊清單。 (HLSManifestResolver)
* 開始從以下位置生成變型清單：內容URL。 （變體）
* 開始將廣告聯繫到資訊清單中。 (VODHLSResolver)
* 嘗試在`HH:MM:SS`處插入廣告：AdPlacement \[adManifestURL=廣告資訊清單URL, durationSeconds= seconds, ignore= ignore, redirectAd= redirect ad, priority= priority.\] \(HLSManifestResolver\)
* 由於無效的時間軸而無法取得廣告——傳回不含廣告的內容。 (VOD)
* 無法取得廣告——傳回不含廣告的內容。 (VOD)
* 無法取得廣告查詢，且未提供內容URL。 (VOD)
* 收到有效的URL。 （VOD/變型）
* 找不到變體M3U8。 （變體）

### TRACE播放進度記錄{#trace-playback-progress-records}

資訊清單伺服器在接收有關伺服器端追蹤工作流程期間播放進度的訊號時，產生此類記錄。 `TRACE_PLAYBACK_PROGRESS`以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|---|---|---|
| 狀態 | 字串 | HTTP狀態代碼 |
| 頻寬 | 整數 | 串流的頻寬 |
| pts | 整數 | 串流中的PTS時間 |
| ms_time | 整數 | 資訊清單伺服器產生追蹤URL的時間 |
| url | 字串 | 重新導向URL |
| **Header_** user_agent | 字串 | HTTP User-Agent標題 |
| **header_** dnt | 整數 | HTTP do-not-track標題 |
| **effective_** remote_address | 字串 | IPv4有效遠程地址 |
| **you** remote_address | 字串 | IPv4遠程地址 |

**最後** 四個欄位是選用的。

## 多位速率串流{#multiple-bitrate-streams}

用戶端廣告插入要求通常會在變數的M3U8格式播放清單中指定多個位元速率。 資訊清單伺服器會產生並傳回新的變型M3U8檔案，其中包含每個位元速率的個別M3U8連結。 它也會產生唯一的群組ID，將這些M3U8系結在一起。

資訊清單伺服器使用用戶端的BootstrapURL請求中的資訊來擷取內容變體播放清單。 它產生包含串流層級內容之資訊清單伺服器連結的新變型播放清單。 用戶端會使用這些項目來建構廣告插入請求。 資訊清單伺服器的串流層級內容連結具有下列格式：

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/**
vod資訊清單伺服器會根據內容的播放清單類型來設定此值：即時／線性(
`#EXT-X-PLAYLIST-TYPE:EVENT`)或VOD(`#EXT-X-PLAYLIST-TYPE:VOD`)

* **PublisherAssetIDPublisher針對BootstrapURL要求中提供之特定內容的唯一ID。**


* **轉**
譯資訊清單伺服器會根據 
`BANDWIDTH` 值，並使用它來比對廣告的位元速率與內容的位元速率。廣告位元速率不得超過內容的位元速率，除非具有最低位元速率的廣告轉譯如此。

* **groupIDT**
manifest伺服器會產生此值，並使用它來確保廣告放置一致，不論用戶端要求廣告的位元速率轉譯為何。

* **位元速率串流的base64編碼URL資訊**
清單伺服器URL安全的base64會編碼內容串流的絕對URL。每個串流都有其專屬的URL。

* **查詢**
參數BootstrapURL請求中提供的查詢參數。
