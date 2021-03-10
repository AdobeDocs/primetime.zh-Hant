---
title: 資訊清單伺服器除錯工具
description: 資訊清單伺服器除錯工具
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiqdonotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# 資訊清單伺服器除錯工具{#manifest-server-debugging-tool}

除錯工具可讓發佈者透過在HTTP標題中即時檢查資訊清單伺服器傳回的除錯資訊，或在需要更詳細的資訊時，檢查事實後的工作階段記錄，來調查可能代價昂貴的廣告插入問題。 Adobe合作夥伴（例如Akamai）可使用此工具除錯其與Primetime廣告決策的整合。

此工具支援任何主要資訊清單伺服器與追蹤組態的除錯與插入問題：

* 使用播放器以TVSDK為基礎的用戶端追蹤。
* 使用非以TVSDK為基礎的播放器進行用戶端追蹤。
* 伺服器端追蹤。

若要支援上述所有情況，此工具不需要或使用播放器發行者代碼。

當您啟動資訊清單伺服器工作階段時，可以在請求URL上設定參數，要求其記錄除錯資訊。 使用該參數的不同值，您也可以要求資訊清單伺服器在HTTP標題中傳回指定的除錯資訊片段，但標題只能包含有限的資訊量。 您可以從Adobe獲取憑據以訪問完整的日誌檔案，該日誌檔案由manifest伺服器定期（例如，每小時）保存到歸檔伺服器上。 一旦您擁有該伺服器的認證後，就可以隨時直接存取。

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## 調試工具選項{#debugging-tool-options}

在叫用除錯工具時，您有數個選項可供選擇，以瞭解資訊清單伺服器在HTTP標題中傳回的資訊。 這些選項不會影響清單伺服器在記錄檔中的位置。

### 指定ptdebug {#specifying-ptdebug}

在啟動資訊清單伺服器工作階段的除錯記錄時，您可將ptdebug參數新增至請求URL，以指定資訊清單伺服器在HTTP標題中傳回的下列選項：

* ptdebug=true除`TRACE_HTTP_HEADER`和`TRACE_AD_CALL`記錄中大多數`call/response data`以外的所有記錄。
* ptdebug=AdCall OnlyTRACE_AD_*type*(例如TRACE_AD_CALL)記錄。
* ptdebug=僅標題TRACE_HTTP_HEADER記錄。

這些選項不會影響清單伺服器在記錄檔中的位置。 您無法控制這一點，但記錄檔是文字檔，因此您可以套用各種工具來擷取並重新格式化您感興趣的資訊。

以下是`ptdebug=Header`時傳回的HTTP標題範例。 某些十六進位數字的長字串會由`. . .`取代，以清楚說明問題。

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

## 日誌記錄的格式{#formats-of-log-records}

每個記錄都有一個類型和一組欄位，其中有些欄位可能是可選的。 直到記錄類型的所有記錄欄位都相同。 它們會提供作業的時間戳記和資訊。 記錄類型可識別記錄的事件類型，而後續欄位則提供記錄事件的相關資訊。

日誌記錄的結構如下：

`datetime request_id session_id zone_id record_type` *其他欄位。*

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 日期時間 | 字串 | 時間戳記 |
| request_id | 字串 | 資訊清單伺服器使用的請求ID（unix時間戳記） |
| session_id | 字串 | 資訊清單伺服器使用的工作階段ID |
| zone_id | 整數 | 區域ID |
| record_type | 字串 | 記錄的事件類型 |
| 其他欄位 | *** | 取決於事件類型 |

### TRACE_REQUEST_INFO記錄{#trace-request-info-records}

此類型的記錄記錄HTTP請求的結果。 TRACE_REQUEST_INFO以外的欄位按表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| request_method | 字串 | HTTP方法(GET或POST) |
| request_uri | 字串 | HTTP請求URI（無主機） |
| request_length | 整數 | 請求長度（位元組） |
| response_length | 整數 | 回應長度（位元組） |
| δ | 整數 | 處理請求的時間（毫秒） |
| module_type | 字串 | 變體、串流或VOD |
| remote_address_aud_client_ip | 字串 | （請參閱附註） |
| remote_address_x_fwd_for_hdr_key | 字串 | （請參閱附註） |
| remote_host_port | 字串 | （請參閱附註） |

>[!NOTE]
>
>最後三個欄位是選用的。

例如：

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER記錄{#trace-http-header-records}

在資訊清單伺服器與用戶端、廣告伺服器或內容伺服器之間進行HTTP呼叫期間交換的此類記錄記錄HTTP標頭。 TRACE_HTTP_HEADER以外的欄位以表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| request_type | 字串 | 請求類型（MAIN或UNKNOWN） |
| request_response | 字串 | 回應標題（請求或回應） |
| header_name | 字串 | HTTP標題名稱 |
| header_value | 字串 | Base64編碼的HTTP標頭值 |

>[!NOTE]
>
>request_type和header_value欄位為選用。

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

### TRACEAD_CALL記錄{#trace-ad-call-records}

此類型的記錄會記錄資訊清單伺服器和要求的結果。 TRACE_AD_CALL以外的欄位以表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| request_duration | 整數 | 請求到回應的時間（毫秒） |
| ad_server_query_url | 字串 | 廣告呼叫的URL，包括查詢參數 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器回應（若未指定，則為Auditude） |
| avail_id | 字串 | 可用的ID，來自內容資訊清單檔案中的廣告提示（VOD的N/A） |
| avail_duration | 數字 | 可用的持續時間（秒），來自內容資訊清單檔案中的廣告提示（VOD為N/A） |
| ad_server_response | 字串 | 來自廣告伺服器的Base64編碼回應 |

例如：

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT、TRACE_AD_RESOLVE和TRACE_AD_REDIRECT記錄{#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

此類型的記錄會記錄記錄類型所指示之廣告請求的結果。 記錄類型以外的欄位按表中顯示的順序顯示，以制表符分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| avail_id | 字串 | 可用的ID，來自內容資訊清單檔案（即時）中的廣告提示，或來自資訊清單伺服器(VOD) |
| ad_type | 字串 | 廣告類型（直接或重新導向） |
| ad_duration | 整數 | 來自廣告伺服器回應的廣告持續時間（秒） |
| ad_content_url | 字串 | 來自廣告伺服器回應的廣告資訊清單檔案的URL |
| ad_content_url_actual | 字串 | 已插入廣告資訊清單檔案的URL。 TRACE_AD_REDIRECT為空。 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器回應（若未指定，則為Auditude） |
| ad_id | 字串 | 來自廣告伺服器回應的廣告ID |
| creative_id | 字串 | 來自廣告節點、來自廣告伺服器回應的創作者ID |
| ad_call_id | 字串 | 未使用。 留待日後使用。 |
| δ | 整數 | 此事件所花費的時間（毫秒） |
| misc | 字串 | 跳過廣告的原因 |

>[!NOTE]
>
>ad_content_url_actual、ad_call_id和misc欄位為選用。

對於TRACE_AD_RESOLVE和TRACE_AD_INSERT，如果有轉碼廣告，則ad_content_url_actual欄位中的URL會用於轉碼廣告。 否則，TRACE_AD_RESOLVE的欄位為空，或者TRACE_AD_INSERT的ad_content_url相同。

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

### TRACE_TRACKING_URL記錄{#trace-tracking-url-records}

此類型的記錄會記錄資訊清單伺服器和要求的結果。 TRACE_TRACKING_URL以外的欄位，依表格中顯示的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| pts | 數字 | 程式時間戳。 呼叫URL的影片時間。 |
| ad_system | 字串 | 廣告系統（auditude或自由輪） |
| url | 字串 | URL pinged |
| 狀態 | 字串 | 從ping返回的HTTP狀態 |

例如：

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE轉碼_RODCING_NO_MEDIA_TO_TRANSCODE記錄{#trace-transcoding-no-media-to-transcode-records}

此類型的記錄記錄遺失廣告創意。 表中只會出現TRACE_DROCKINING_NO_MEDIA_TO_TRANSCODE以外的欄位。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| ad_id | 字串 | 完全限定的廣告ID `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID:`PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]`協定：AUDITUDE, VAST) |

### TRACE轉碼請求記錄{#trace-transcoding-requested-records}

此類型的記錄記錄資訊清單伺服器傳送至CRS的轉碼請求結果。 除TRACE_DROCKINING_REQUESTED之外的欄位以表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| ad_id | 字串 | 完全限定的廣告ID |
| ad_manifest_url | 字串 | 來自廣告伺服器回應的廣告資訊清單檔案的URL |
| creative_type | 字串 | 媒體類型 |
| 旗標 | 字串 | ID3指出轉碼請求是否包含新增ID3標籤的請求 |
| target_duration | 字串 | 轉碼創意素材的目標持續時間（秒） |

### TRACE_TRACKING_REQUEST記錄{#trace-tracking-request-records}

此類型的記錄會指出執行伺服器端追蹤的要求。 TRACE_TRACKING_REQUEST以外的欄位會依表格中的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| tracking_url_count | 整數 | 追蹤URL的數量 |
| start | 浮水 | PTS碎片開始時間（秒，精確到毫秒） |
| end | 浮水 | PTS片段結束時間（秒數，精確到毫秒） |

### TRACE_TRACKING_REQUEST_URL記錄{#trace-tracking-request-url-records}

此類型的記錄提供伺服器端追蹤的追蹤URL。 TRACE_TRACKING_REQUEST_URL以外的欄位以表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 時間戳記 | 浮水 | 播放工作階段內ping追蹤URL的時間（秒數，精確度為。001） |
| ad_system | 字串 | 廣告系統（例如auditude） |
| url | 字串 | Ping的URL |

### TRACE_WEBVTT_REQUEST記錄{#trace-webvtt-request-records}

此類型記錄會要求資訊清單伺服器為WEBVTT標題提供資訊。 TRACE_WEBVTT_REQUEST以外的欄位按表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| vtt_uri | 字串 | 請求的URL |
| start | 浮水 | 分割開始時間（秒數，精確到毫秒） |
| end | 浮水 | 分割結束時間（秒數，精確到毫秒） |

### TRACE_WEBVTT_RESPONSE記錄{#trace-webvtt-response-records}

將``type ````of ````manifest ``伺服器``sends ``記錄到`` `answer` ````clients ````requests ```for```WEBVTT ``標題。 ``responses ``TRACE_WEBVTT_RESPONSE &#39;&#39;以外的欄位按表中顯示的順序顯示，分隔為`by`頁籤。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| 響應 | 字串 | 傳送給用戶端的Base64編碼回應 |

### TRACE_WEBVTT_SOURCE記錄{#trace-webvtt-source-records}

此類型的記錄會記錄資訊，以回應資訊清單伺服器對WEBVTT標題的要求。 TRACE_WEBVTT_SOURCE以外的欄位以表中顯示的順序顯示，並以頁籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回的HTTP狀態代碼 |
| 來源 | 字串 | Base64編碼的原始VTT內容 |


### TRACE_MISC記錄{#trace-misc-records}

此類型的記錄可讓資訊清單伺服器記錄未計畫在擷取廣告時的事件和資訊。 TRACE_MISC以外的欄位由消息字串組成。 可能出現的訊息包括：

* 已忽略廣告：AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*,durationSeconds=*秒*,ignore=*ignore*,redirectAd=*redirectAd*, prioriryoritory=*priority&lt;a9/*
* 廣告位置傳回null。
* 成功銜接廣告。
* 廣告呼叫失敗：*錯誤消息*。
* 新增User-Agent以擷取原始資訊清單：*user-agent*。
* 新增Cookie以擷取原始資訊清單：[cookie]
* 錯誤的URL *請求的URL錯誤消息*。 （無法解析變型URL）
* 呼叫的url:URL *獲得返回：響應代碼*。 （即時URL）
* 呼叫的url:URL *返回代碼：響應代碼*。 (VOD URL)
* 解決廣告時發現衝突：其中一個——中間輥開始端或中間輥結束端落在中間輥(VOD)中包含的前輥或前輥內。
* URI的處理程式檢測到未處理的異常：*請求URL*。
* 已完成變型資訊清單的產生。 （變體）
* 已完成變型資訊清單的產生。
* 處理VAST重新導向*重新導向URL *錯誤：*錯誤消息*。
* 無法擷取&#x200B;*廣告資訊清單URL*&#x200B;的廣告播放清單。
* 無法產生目標資訊清單。 (HLSManifestResolver)
* 無法解析第一個廣告呼叫回應：*錯誤消息*。
* 無法處理*GET|POST*路徑請求：*請求URL*。 （即時/VOD）
* 無法處理即時資訊清單請求：*請求URL*。 （即時）
* 無法傳回變型資訊清單：*錯誤消息*。
* 無法驗證組ID:*群組ID*。
* 正在擷取原始資訊清單：*內容URL*。 （即時）
* 遵循廣泛的重新導向：*重新導向URL*。
* 找到空的可用。 (VOD)
* 找到*數字*廣告。 (VOD)
* 收到HTTP請求。 （第一條訊息）
* 忽略廣告，因為廣告回應持續時間（*廣告回應持續時間*秒）與實際廣告持續時間（*實際持續時間*秒）之間的差異大於限制。 (HLSManifestResolver)
* 忽略未提供ID值的可用值。 (GroupAdResolver.java)
* 正在忽略提供無效時間值的可用：*time *for availId = *avail ID*。
* 正在忽略提供無效持續時間值的可用值：*duration *for availId = *avail ID*。
* 初始化新會話。 （變體）
* 無效的HTTP方法。 一定是GET。 (VOD)
* 無效的HTTP方法。 追蹤要求必須是GET。 （即時）
* 無效的URL *請求的URL錯誤消息*。 （變體）
* 無效的組。 (HLSManifestResolver)
* 請求無效。 標題不是有效的追蹤請求。 (VOD)
* 請求無效。 標題請求必須在會話建立後進行。 (VOD)
* 請求無效。 必須在建立工作階段後提出追蹤要求。 (VOD)
* 過載組ID的伺服器實例無效：*群組ID*。 （即時）
* 已達到VAST重定向的限制- *number*。
* 進行廣告呼叫：*廣告呼叫URL*。
* 找不到以下項目的清單：*內容URL*。 （即時）
* 找不到可用ID的匹配可用值：*可用ID*。 (HLSManifestResolver)
* 找不到播放會話。 (HLSManifestResolver)
* 處理資訊清單&#x200B;*內容URL*&#x200B;的VOD請求。
* 正在處理變型。
* 處理資訊清單&#x200B;*內容URL*&#x200B;的標題請求。
* 正在處理追蹤請求。 (VOD)
* 重新導向廣告回應空白。 (VASTStAX)
* 請求：*URL*。
* 傳回GET請求的錯誤回應，因為找不到播放作業。 (VOD)
* 因內部伺服器錯誤而傳回GET要求的錯誤回應。
* 針對指定無效資產的GET請求傳回錯誤回應：*廣告請求ID*。 (VOD)
* 傳回指定無效或空白群組ID之GET要求的錯誤回應：*群組ID*。 (VOD)
* 傳回指定無效追蹤位置值之GET要求的錯誤回應。 (VOD)
* 以無效語法傳回GET請求的錯誤回應- *請求URL*。 （即時/VOD）
* 使用不支援的HTTP方法傳回請求的錯誤回應：*GET|POST*。 （即時/VOD）
* 從快取傳回資訊清單。 (VOD)
* 伺服器過載。 不需要廣告插圖請求即可繼續。 （變體）
* 開始產生目標資訊清單。 (HLSManifestResolver)
* 開始從以下位置生成變型清單：*內容URL*。 （變體）
* 開始將廣告聯繫到資訊清單中。 (VODHLSResolver)
* 嘗試在`HH:MM:SS`處插入廣告：AdPlacement \[adManifestURL=*廣告資訊清單URL*,durationSeconds=*秒*,ignore=*ignore*,redirectAd=*redirect ad*, pririoriority=*優先順序*。]
* 由於無效的時間軸而無法取得廣告——傳回不含廣告的內容。 (VOD)
* 無法取得廣告——傳回不含廣告的內容。 (VOD)
* 無法取得廣告查詢，且未提供內容URL。 (VOD)
* 收到有效的URL。 （VOD/變型）
* 找不到變體M3U8。 （變體）

### TRACE_TRACKING_URL記錄{#trace-tracking-url-records-1}

資訊清單伺服器在伺服器端追蹤工作流程期間呼叫追蹤URL後，會產生此類記錄。 TRACE_TRACKING_URL以外的欄位，依表格中顯示的順序顯示，並以標籤分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| pts | 數字 | 串流中的PTS時間 |
| ad_system | 字串 | 廣告的廣告系統（auditude或自由輪） |
| url | 字串 | URL pinged |
| state | 字串 | HTTP狀態代碼 |

### TRACE播放進度記錄{#trace-playback-progress-records}

資訊清單伺服器在接收有關伺服器端追蹤工作流程期間播放進度的訊號時，產生此類記錄。 TRACE_PLAYBACK_PROGRESS以外的欄位按表中顯示的順序顯示，並以制表符分隔。

| 欄位 | 類型 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | HTTP狀態代碼 |
| 頻寬 | 整數 | 串流的頻寬 |
| pts | 整數 | 串流中的PTS時間 |
| ms_time | 整數 | 資訊清單伺服器產生追蹤URL的時間 |
| url | 字串 | 重新導向URL |
| header_user_agent | 字串 | HTTP User-Agent標題 |
| header_dnt | 整數 | HTTP do-not-track標題 |
| effective_remote_address | 字串 | IPv4有效遠程地址 |
| remote_address | 字串 | IPv4遠程地址 |

>[!NOTE]
>
>最後四個欄位為選用。

## 實用資源{#helpful-resources}

* 請參閱[Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html)頁面的完整說明檔案。
