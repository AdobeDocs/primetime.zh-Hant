---
title: 清單伺服器調試工具
description: 清單伺服器調試工具
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiqdonotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# 清單伺服器調試工具 {#manifest-server-debugging-tool}

調試工具使發佈者能夠通過檢查清單伺服器在HTTP標頭中即時返回的調試資訊來調查可能成本高昂的廣告插入問題，或者當需要更詳細的資訊時，檢查事實後的會話日誌。 Adobe合作夥伴，如Akamai，可以使用該工具調試他們與黃金時段廣告決策的整合。

該工具支援在任何主清單伺服器和跟蹤配置中調試和插入問題：

* 基於TVSDK的播放器的客戶端跟蹤。
* 不基於TVSDK的播放器的客戶端跟蹤。
* 伺服器端跟蹤。

要支援所有這些情況，該工具不需要或使用播放器發佈者代碼。

啟動清單伺服器會話時，可以在請求URL上設定參數，要求它記錄調試資訊。 使用該參數的不同值，您還可以要求清單伺服器在HTTP標頭中返回指定的調試資訊，但標頭只能包含有限量的資訊。 您可以從Adobe獲取憑據以訪問完整的日誌檔案，清單伺服器會定期（例如，每小時）將這些日誌檔案保存在存檔伺服器上。 一旦您擁有了該伺服器的憑據，就可以隨時直接訪問它。

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## 調試工具選項 {#debugging-tool-options}

調用調試工具時，您有幾個選項，用於瞭解清單伺服器在HTTP標頭中返回的資訊。 這些選項不會影響清單伺服器在日誌檔案中的位置。

### 指定ptdebug {#specifying-ptdebug}

在啟動清單伺服器會話的調試日誌記錄時，可以將ptdebug參數添加到請求URL，以指定清單伺服器在HTTP標頭中返回的資訊的以下選項：

* ptdebug=true除外的所有記錄 `TRACE_HTTP_HEADER` 大多數 `call/response data` 從 `TRACE_AD_CALL` 記錄。
* ptdebug=AdCall僅TRACE_AD_*類型* (例如，TRACE_AD_CALL)記錄。
* ptdebug=僅標頭TRACE_HTTP_HEADER記錄。

這些選項不會影響清單伺服器在日誌檔案中的位置。 您無法控制這一點，但日誌檔案是文本檔案，因此您可以應用多種工具來提取和重新格式化您感興趣的資訊。

以下是HTTP標頭的示例 `ptdebug=Header`。 某些十六進位數字的長字串由 `. . .` 為了澄清。

```
X-ADBE-AI-DBG-1 TRACE_MISC    HTTP request received
X-ADBE-AI-DBG-2 TRACE_MISC    Processing Variant
X-ADBE-AI-DBG-3 TRACE_MISC    Valid URL received.
X-ADBE-AI-DBG-4 TRACE_MISC    Initialize new session
X-ADBE-AI-DBG-5 TRACE_MISC    Requesting: /auditude/variant/pubAsset/aHR0cDovL . . .m3u8
 ?u=cecebae . . .&z=189962&pttrackingmode=simple&pttrackingversion=v1
 &ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true
X-ADBE-AI-DBG-6  TRACE_HTTP_HEADER  MAIN  REQUEST  Host    bWFuaWZl. . .
X-ADBE-AI-DBG-7  TRACE_HTTP_HEADER  MAIN  REQUEST  Connection       Y2xvc2U=
X-ADBE-AI-DBG-8  TRACE_HTTP_HEADER  MAIN  REQUEST  Accept   dGV4dC. . .
X-ADBE-AI-DBG-9  TRACE_HTTP_HEADER  MAIN  REQUEST  Cookie   c3NhaT. . .
X-ADBE-AI-DBG-10 TRACE_HTTP_HEADER  MAIN  REQUEST  User-Agent       TW96aWxs. . .
X-ADBE-AI-DBG-11 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Language  ZW4tdXM=
X-ADBE-AI-DBG-12 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Encoding  Z3ppcCwg. . .=
X-ADBE-AI-DBG-13 TRACE_REQUEST_INFO  200   GET
 /auditude/variant/pubAsset/aHR0cD. . ..m3u8
 ?u=cecebae72a919de350b9ac52602623f3&z=189962&pttrackingmode=simple
 &pttrackingversion=v1&ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true   0 0 0   Variant  NA  null  null  127.0.0.1:43357
X-ADBE-AI-DBG-14 TRACE_HTTP_HEADER  MAIN  RESPONSE Content-Type     YXBwbG. . .
X-ADBE-AI-DBG-15 TRACE_HTTP_HEADER  MAIN  RESPONSE Cache-Control    bm8tY2. . .
X-ADBE-AI-DBG-16 TRACE_HTTP_HEADER  MAIN  RESPONSE Access-Control-Allow-Origin    Kg==
X-ADBE-AI-DBG-17 TRACE_MISC   Done
```

## 日誌記錄的格式 {#formats-of-log-records}

每個日誌記錄都有一個類型和一組欄位，其中有些欄位可能是可選的。 記錄類型之前的所有記錄的欄位相同。 它們提供有關會話的時間戳和資訊。 記錄類型標識記錄的事件類型，後續欄位提供有關記錄事件的資訊。

日誌記錄的結構如下：

`datetime request_id session_id zone_id record_type` *其他欄位。*

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 日期 | 字串 | 時間戳 |
| 請求ID | 字串 | 清單伺服器使用的請求ID（unix時間戳） |
| 會話ID | 字串 | 清單伺服器使用的會話ID |
| 區域ID | 整數 | 區域ID |
| 記錄類型 | 字串 | 正在記錄的事件類型 |
| 其他欄位 | *** | 取決於事件類型 |

### TRACE_REQUEST_INFO記錄 {#trace-request-info-records}

此類型的記錄記錄HTTP請求的結果。 TRACE_REQUEST_INFO以外的欄位按表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| 請求方法 | 字串 | HTTP方法(GET或POST) |
| 請求_uri | 字串 | HTTP請求URI（無主機） |
| 請求長度 | 整數 | 請求長度（位元組） |
| 響應長度 | 整數 | 響應長度（位元組） |
| 三角 | 整數 | 處理請求的時間（毫秒） |
| 模組類型 | 字串 | 變型、流或VOD |
| 遠程_地址_aud_client_ip | 字串 | （請參閱附註） |
| remote_address_x_fwd_for_hdr_key | 字串 | （請參閱附註） |
| 遠程主機埠 | 字串 | （請參閱附註） |

>[!NOTE]
>
>最後三個欄位是可選的。

例如：

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER記錄 {#trace-http-header-records}

在清單伺服器和客戶端、廣告伺服器或內容伺服器之間的HTTP調用期間交換的此類型日誌HTTP標頭的記錄。 TRACE_HTTP_HEADER之外的欄位按表中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 請求類型 | 字串 | 請求類型（主或未知） |
| 請求響應 | 字串 | 響應標頭（請求或響應） |
| 標題名稱 | 字串 | HTTP標頭名稱 |
| 標頭_值 | 字串 | Base64編碼的HTTP標頭值 |

>[!NOTE]
>
>request_type和header_value欄位是可選的。

例如：

```
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_MISC
    Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST Cookie  aGRu. . .
2015-03-25T06:10:00.928Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST User-Agent  TW96aW. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Server  bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Content-Type    YXBwb. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Last-Modified   V2VkL. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  ETag    IjIyY2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Vary    QWNjZXB. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Cache-Control   bWF4LW. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Expires V2VkL. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Date    V2VkLCA. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Age MQ==
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Via MS4xIH. . .
```

### TRACE_AD_CALL記錄 {#trace-ad-call-records}

此類型的記錄記錄清單伺服器和請求的結果。 TRACE_AD_CALL以外的欄位按表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| 請求持續時間 | 整數 | 從請求到響應的時間（毫秒） |
| ad_server_query_url | 字串 | 廣告調用的URL，包括查詢參數 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器響應（如果未指定，則為Audity） |
| 可用ID | 字串 | 從內容清單檔案中的廣告提示獲得的可用ID（N/A用於VOD） |
| 可用持續時間 | 數 | 可用的持續時間（秒），來自內容清單檔案中的廣告提示（N/A用於VOD） |
| ad_server_response | 字串 | 來自ad伺服器的Base64編碼響應 |

例如：

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT、TRACE_AD_RESOLVE和TRACE_AD_REDIRECT記錄 {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

此類型的記錄記錄記錄類型所指示的廣告請求的結果。 記錄類型以外的欄位按表中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| 可用ID | 字串 | 可用的ID，來自內容清單檔案（即時）中的廣告提示或來自清單伺服器(VOD) |
| ad_type | 字串 | 廣告類型（直接或重定向） |
| ad_duration | 整數 | 廣告持續時間（秒），來自廣告伺服器響應 |
| ad_content_url | 字串 | 廣告的清單檔案的URL，來自廣告伺服器響應 |
| ad_content_url_actual | 字串 | 插入廣告的清單檔案的URL。 TRACE_AD_REDIRECT為空。 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器響應（如果未指定，則為Audity） |
| ad_id | 字串 | 廣告的ID，來自廣告伺服器響應 |
| creative_id | 字串 | 創作者的ID，從ad節點，從ad伺服器響應 |
| ad_call_id | 字串 | 未使用。 保留供將來使用。 |
| 三角 | 整數 | 此事件所花費的時間（毫秒） |
| 雜項 | 字串 | 跳過廣告的原因 |

>[!NOTE]
>
>ad_content_url_actual、ad_call_id和misc欄位是可選的。

對於TRACEAD_RESOLVE和TRACEAD_INSERT,ad_content_url_actual欄位中的URL用於轉碼ad（如果有）。 否則，TRACEAD_RESOLVE的欄位為空，或者與TRACEAD_INSERT的ad_content_url相同。

例如：

```
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

### TRACE_跟蹤_URL記錄 {#trace-tracking-url-records}

此類型的記錄記錄清單伺服器和請求的結果。 TRACE_TRACKING_URL以外的欄位按表中顯示的順序顯示，並以制表符分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 點 | 數 | 程式時間戳。 調用URL的視頻內時間。 |
| ad_system | 字串 | 廣告系統（音頻或自由輪） |
| url | 字串 | URL已ping |
| 狀態 | 字串 | 從ping返回的HTTP狀態 |

例如：

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE轉碼_NO_MEDIA_TO_TRANSCODE記錄 {#trace-transcoding-no-media-to-transcode-records}

此類記錄記錄缺少廣告創意。 表中將顯示除TRACE轉碼NOMEDIATOTRANSCODE之外的唯一欄位。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| ad_id | 字串 | 完全限定廣告ID `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` 協定：巨幅) |

### TRACE_轉碼_請求記錄 {#trace-transcoding-requested-records}

此類型的記錄記錄清單伺服器發送到CRS的轉碼請求的結果。 除TRACE_TRONCIDING_REQUESTED之外的欄位按表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| ad_id | 字串 | 完全限定廣告ID |
| ad_manifest_url | 字串 | 廣告的清單檔案的URL，來自廣告伺服器響應 |
| creative_type | 字串 | 介質類型 |
| 標誌 | 字串 | ID3指示轉碼請求是否包括添加ID3標籤的請求 |
| 目標持續時間 | 字串 | 轉碼創作的目標持續時間（秒） |

### TRACE_跟蹤_請求記錄 {#trace-tracking-request-records}

此類型的記錄表示請求執行伺服器端跟蹤。 TRACE_TRACKING_REQUEST以外的欄位按表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 跟蹤_url_計數 | 整數 | 跟蹤URL數 |
| 開始 | 浮 | PTS片段開始時間（秒，毫秒精度） |
| 端 | 浮 | PTS片段結束時間（秒，毫秒精度） |

### TRACE_跟蹤_請求_URL記錄 {#trace-tracking-request-url-records}

此類型的記錄提供用於伺服器端跟蹤的跟蹤URL。 TRACE_TRACKING_REQUEST_URL之外的欄位按表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 時間戳 | 浮 | 播放會話中ping跟蹤URL的時間（秒，精度為。001） |
| ad_system | 字串 | 廣告系統（例如，審級） |
| url | 字串 | 要ping的URL |

### TRACE_WEBVT_REQUEST記錄 {#trace-webvtt-request-records}

此類型的日誌記錄請求清單伺服器為WEBVTT標題生成的。 TRACE_WEBVTT_REQUEST之外的欄位按表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| vtt_uri | 字串 | 請求的URL |
| 開始 | 浮 | 分割開始時間（秒，毫秒精度） |
| 端 | 浮 | 拆分結束時間（秒，毫秒精度） |

### TRACE_WEBVTT_RESPONSE記錄 {#trace-webvtt-response-records}

記錄 ``of ``這個 ``type ``日誌 ``responses ``這樣 ``manifest ``伺服器 ``sends ``至 ``clients ``在 `` `answer` ``至 ``requests `` `for` ``WEBVTT ``標題。 TRACE_WEBVTT_RESPONSE &quot;之外的欄位按表中顯示的順序顯示，分隔 `by`頁籤。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| 響應 | 字串 | 已將Base64編碼的響應發送給客戶端 |

### TRACE_WEBVT_SOURCE記錄 {#trace-webvtt-source-records}

此類型的記錄記錄對清單伺服器為WEBVTT標題所發出的請求的日誌響應。 TRACE_WEBVTT_SOURCE之外的欄位按表中顯示的順序顯示，並以制表符分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 返回的HTTP狀態代碼 |
| 源 | 字串 | Base64編碼的原始VTT內容 |


### TRACE_MISC記錄 {#trace-misc-records}

此類記錄使清單伺服器能夠記錄在接收廣告時未計畫的事件和資訊。 TRACE_MISC之外的欄位由消息字串組成。 可能出現的消息包括：

* 已忽略Ad:AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*,durationSeconds=*秒*，忽略=*忽略*，重定向廣告=*重定向廣告*，優先順序=*優先順序*
* 廣告放置返回空值。
* 廣告成功縫製。
* 廣告調用失敗： *錯誤消息*。
* 添加User-Agent以獲取原始清單： *用戶代理*。
* 添加cookie以獲取原始清單： [餅]
* 錯誤URL *請求的URL錯誤消息*。 （無法分析變型URL）
* 調用的URL:URL *得到返回：響應代碼*。 （即時URL）
* 調用的URL:URL *返回代碼：響應代碼*。 (VOD URL)
* 解決廣告時發現衝突：中輥起動或中輥端之一位於中輥(VOD)中包含的預輥或預輥內。
* 檢測到URI的處理程式引發的未處理的異常： *請求URL*。
* 生成變型清單已完成。 （變型）
* 生成變型清單已完成。
* 處理VAST重定向*重定向URL時出現異常*錯誤： *錯誤消息*。
* 無法獲取廣告的播放清單 *廣告清單URL*。
* 未能生成目標清單。 (HLSManifestResolver)
* 無法分析第一個廣告呼叫響應： *錯誤消息*。
* 無法處理*GET|POST*路徑請求： *請求URL*。 （即時/視頻點播）
* 無法處理即時清單請求： *請求URL*。 （即時）
* 無法返回變型清單： *錯誤消息*。
* 無法驗證組ID: *組ID*。
* 正在獲取原始清單： *內容URL*。 （即時）
* 遵循VAST重定向： *重定向URL*。
* 找到空的可用。 (VOD)
* 找到*號*廣告。 (VOD)
* 收到HTTP請求。 （第一條消息）
* 忽略ad，因為ad響應持續時間（*ad響應持續時間*秒）和實際廣告持續時間（*實際持續時間*秒）之間的差值大於限制。 (HLSManifestResolver)
* 忽略未提供ID值的可用。 (GroupAdResolver.java)
* 忽略提供無效時間值的可用：*可用ID的時間* *可用ID*。
* 忽略提供無效持續時間值的可用：*可用ID的持續時間*= *可用ID*。
* 初始化新會話。 （變型）
* HTTP方法無效。 一定是GET。 (VOD)
* HTTP方法無效。 跟蹤請求必須是GET。 （即時）
* 無效的URL *請求的URL錯誤消息*。 （變型）
* 組無效。 (HLSManifestResolver)
* 請求無效。 標題不是有效的跟蹤請求。 (VOD)
* 請求無效。 必須在會話建立後發出標題請求。 (VOD)
* 請求無效。 必須在會話建立後發出跟蹤請求。 (VOD)
* 重載組ID的伺服器實例無效： *組ID*。 （即時）
* 已達到VAST重定向限制 —  *數*。
* 進行廣告呼叫： *廣告呼叫URL*。
* 未找到以下項的清單： *內容URL*。 （即時）
* 找不到可用ID的匹配可用： *可用ID*。 (HLSManifestResolver)
* 未找到回放會話。 (HLSManifestResolver)
* 處理清單的VOD請求 *內容URL*。
* 正在處理變型。
* 正在處理清單的標題請求 *內容URL*。
* 正在處理跟蹤請求。 (VOD)
* 重定向廣告響應為空。 (VASTStAX)
* 請求： *URL*。
* 返回GET請求的錯誤響應，因為未找到回放會話。 (VOD)
* 由於內部伺服器錯誤，正在為GET請求返回錯誤響應。
* 為指定無效資產的GET請求返回錯誤響應： *廣告請求ID*。 (VOD)
* 為指定無效或空組ID的GET請求返回錯誤響應： *組ID*。 (VOD)
* 為指定無效跟蹤位置值的GET請求返回錯誤響應。 (VOD)
* 返回語法無效的GET請求的錯誤響應 —  *請求URL*。 （即時/視頻點播）
* 使用不支援的HTTP方法返回請求的錯誤響應： *GET|POST*。 （即時/視頻點播）
* 正在從快取返回清單。 (VOD)
* 伺服器已過載。 無需廣告縫合請求即可繼續。 （變型）
* 開始生成目標清單。 (HLSManifestResolver)
* 開始從以下位置生成變型清單： *內容URL*。 （變型）
* 開始將廣告拼接到清單中。 (VODHLSResolver)
* 試圖在 `HH:MM:SS`:AdPlacement \[adManifestURL=*廣告清單URL*,durationSeconds=*秒*，忽略=*忽略*，重定向廣告=*重定向廣告*，優先順序=*優先順序*.\]
* 由於時間軸無效，無法獲取廣告 — 返回沒有廣告的內容。 (VOD)
* 無法獲取廣告 — 返回沒有廣告的內容。 (VOD)
* 無法獲取廣告查詢，未提供內容URL。 (VOD)
* 收到有效的URL。 （VOD/變型）
* 找不到變型M3U8。 （變型）

### TRACE_跟蹤_URL記錄 {#trace-tracking-url-records-1}

清單伺服器在伺服器端跟蹤工作流期間調用跟蹤URL後生成此類記錄。 TRACE_TRACKING_URL以外的欄位按表中顯示的順序顯示，並以制表符分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 點 | 數 | 流內的PTS時間 |
| ad_system | 字串 | 廣告廣告系統（警戒或自由輪） |
| url | 字串 | URL已ping |
| 狀態 | 字串 | HTTP狀態代碼 |

### TRACE_回放_進度記錄 {#trace-playback-progress-records}

清單伺服器在伺服器端跟蹤工作流期間接收關於回放進度的信號時生成這種記錄。 TRACE_PLAYBACK_PROGRESS以外的欄位按表中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | HTTP狀態代碼 |
| 頻寬 | 整數 | 流的頻寬 |
| 點 | 整數 | 流內的PTS時間 |
| ms_time | 整數 | 清單伺服器生成跟蹤URL的時間 |
| url | 字串 | 重定向URL |
| 標頭_用戶_代理 | 字串 | HTTP用戶代理標頭 |
| 標頭_dnt | 整數 | HTTP不跟蹤標頭 |
| 有效_remote_address | 字串 | IPv4有效遠程地址 |
| 遠程地址 | 字串 | IPv4遠程地址 |

>[!NOTE]
>
>最後四個欄位是可選的。

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://helpx.adobe.com/support/primetime.html) 的子菜單。
