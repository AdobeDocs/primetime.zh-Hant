---
title: 資訊清單伺服器偵錯工具
description: 資訊清單伺服器偵錯工具
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


# 資訊清單伺服器偵錯工具 {#manifest-server-debugging-tool}

偵錯工具可讓發佈者檢查資訊清單伺服器在HTTP標題中即時傳回的偵錯資訊，或在需要更詳細資訊時，在事後檢查工作階段記錄，藉此調查可能較昂貴的廣告插入問題。 Akamai等Adobe合作夥伴可以使用此工具來偵錯他們與Primetime ad decisioning的整合。

此工具支援在任何主要資訊清單伺服器和追蹤設定中進行偵錯和插入問題：

* 透過基於TVSDK的播放器進行使用者端追蹤。
* 使用非以TVSDK為基礎的播放器的使用者端追蹤。
* 伺服器端追蹤。

為了支援所有這些情況，該工具不需要或使用播放器發佈程式碼。

當您啟動資訊清單伺服器工作階段時，可以在請求URL上設定引數，以要求它記錄偵錯資訊。 若使用該引數的不同值，您也可以要求資訊清單伺服器傳回HTTP標頭中的指定偵錯資訊片段，但標頭只能包含有限數量的資訊。 您可以從Adobe取得認證，以存取資訊清單伺服器定期（例如，每小時）儲存於封存伺服器上的完整記錄檔。 一旦您擁有該伺服器的認證，您就可以隨時直接存取它。

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## 偵錯工具選項 {#debugging-tool-options}

叫用偵錯工具時，資訊清單伺服器會在HTTP標頭中傳回哪些資訊，有幾個選項。 選項不會影響資訊清單伺服器放置在記錄檔中的內容。

### 指定ptdebug {#specifying-ptdebug}

起始資訊清單伺服器工作階段的偵錯記錄時，您可以將ptdebug引數新增至要求URL，為資訊清單伺服器傳回的HTTP標頭資訊指定下列選項：

* ptdebug=true所有記錄，除了 `TRACE_HTTP_HEADER` 和最多 `call/response data` 從 `TRACE_AD_CALL` 記錄。
* ptdebug=AdCall OnlyTRACE_AD_*type* (例如TRACE_AD_CALL)記錄。
* ptdebug=Header OnlyTRACE_HTTP_HEADER記錄。

選項不會影響資訊清單伺服器放置在記錄檔中的內容。 您對此沒有控制權，但記錄檔是文字檔，因此您可以套用各種工具來擷取和重新格式化您感興趣的資訊。

以下範例為以下情況下傳回的HTTP標頭： `ptdebug=Header`. 某些十六進位數字的長字串會取代為 `. . .` 以求清晰明瞭。

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

## 記錄檔記錄格式 {#formats-of-log-records}

每個記錄檔記錄都有一個型別和一組欄位，其中一些可能是選擇性的。 記錄型別之前的所有記錄的欄位都是相同的。 它們會提供工作階段的時間戳記和資訊。 記錄型別會識別所記錄的事件的型別，而後續欄位會提供有關所記錄事件的資訊。

記錄檔記錄的結構如下：

`datetime request_id session_id zone_id record_type` *其他欄位。*

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 日期時間 | 字串 | 時間戳記 |
| request_id | 字串 | 資訊清單伺服器使用的請求ID （unix時間戳記） |
| session_id | 字串 | 資訊清單伺服器使用的工作階段ID |
| zone_id | 整數 | 區域ID |
| record_type | 字串 | 所記錄的事件的型別 |
| 其他欄位 | *** | 視事件型別而定 |

### TRACE_請求_資訊記錄 {#trace-request-info-records}

此型別的記錄會記錄HTTP請求的結果。 超出TRACE_REQUEST_INFO的欄位會以表格中所示的順序顯示，並以標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| request_method | 字串 | HTTP方法(GET或POST) |
| request_uri | 字串 | HTTP要求URI （不含主機） |
| request_length | 整數 | 要求長度（位元） |
| response_length | 整數 | 回應長度（位元） |
| delta | 整數 | 處理要求的時間（毫秒） |
| 模組型別 | 字串 | 變體、資料流或VOD |
| remote_address_aud_client_ip | 字串 | （請見附註） |
| remote_address_x_fwd_for_hdr_key | 字串 | （請見附註） |
| remote_host_port | 字串 | （請見附註） |

>[!NOTE]
>
>最後三個欄位是選用欄位。

範例：

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER記錄 {#trace-http-header-records}

此型別的記錄會記錄資訊清單伺服器與使用者端、廣告伺服器或內容伺服器之間的HTTP呼叫期間交換的HTTP標頭。 TRACE_HTTP_HEADER以外的欄位會依表格中所示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| request_type | 字串 | 請求型別（主要或未知） |
| request_response | 字串 | 回應標頭（請求或回應） |
| header_name | 字串 | HTTP標頭名稱 |
| header_值 | 字串 | Base64編碼的HTTP標頭值 |

>[!NOTE]
>
>request_type和header_value欄位是選用欄位。

範例：

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

此型別的記錄記錄會記錄資訊清單伺服器和要求的結果。 TRACE_AD_CALL以外的欄位會以表格中顯示的順序顯示，並以索引標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| request_duration | 整數 | 從要求到回應的時間（毫秒） |
| ad_server_query_url | 字串 | 廣告呼叫的URL，包括查詢引數 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器回應（若未指定，則為稽核） |
| avail_id | 字串 | 從內容資訊清單檔案中的廣告提示取得的有效的ID （VOD不適用） |
| avail_duration | 數字 | 從內容資訊清單檔案中的廣告提示取得廣告的持續時間（秒） （VOD不適用） |
| ad_server_response | 字串 | 來自廣告伺服器的Base64編碼回應 |

範例：

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT、TRACE_AD_RESOLVE和TRACE_AD_REDIRECT記錄 {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

此型別的記錄會記錄記錄該記錄型別所指示的廣告請求的結果。 記錄型別以外的欄位會以表格中顯示的順序顯示（以索引標籤分隔）。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| avail_id | 字串 | 從內容資訊清單檔案（即時）中的廣告提示或來自資訊清單伺服器(VOD)的可用的ID |
| ad_type | 字串 | 廣告型別（直接或重新導向） |
| ad_duration | 整數 | 廣告持續時間（秒），來自廣告伺服器回應 |
| ad_content_url | 字串 | 廣告資訊清單檔案的URL，來自廣告伺服器回應 |
| ad_content_url_actual | 字串 | 插入廣告資訊清單檔案的URL。 留空表示TRACE_AD_REDIRECT。 |
| ad_system_id | 字串 | 廣告系統，來自廣告伺服器回應（若未指定，則為稽核） |
| ad_id | 字串 | 廣告ID，來自廣告伺服器回應 |
| creative_id | 字串 | 廣告節點和廣告伺服器回應中的創意ID |
| ad_call_id | 字串 | 未使用。 保留以供日後使用。 |
| delta | 整數 | 此事件花費的時間（毫秒） |
| 雜項 | 字串 | 略過廣告的原因 |

>[!NOTE]
>
>ad_content_url_actual、ad_call_id和其他欄位是選用欄位。

對於TRACE_AD_RESOLVE和TRACE_AD_INSERT，ad_content_url_actual欄位中的URL適用於轉碼廣告（如果可用）。 否則，TRACE_AD_RESOLVE的欄位為空白，或者與TRACE_AD_INSERT的ad_content_url相同。

範例：

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

### TRACE_追蹤_URL記錄 {#trace-tracking-url-records}

此型別的記錄記錄會記錄資訊清單伺服器和要求的結果。 TRACE_TRACKING_URL以外的欄位會以表格中顯示的順序顯示，並以索引標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 分 | 數字 | 程式時間戳記。 在視訊中呼叫URL的時間。 |
| ad_system | 字串 | 廣告系統（auditude或任意輪） |
| url | 字串 | 已釘選的URL |
| 狀態 | 字串 | 從ping傳回的HTTP狀態 |

範例：

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE記錄 {#trace-transcoding-no-media-to-transcode-records}

此型別的記錄會記錄缺少的廣告創意。 除了TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE之外，表格中唯一出現一個欄位。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| ad_id | 字串 | 完整廣告ID `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID： `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` 通訊協定：AUDITUDE，VAST) |

### TRACE_轉碼_要求的記錄 {#trace-transcoding-requested-records}

此型別的記錄會記錄資訊清單伺服器傳送至CRS的轉碼請求結果。 超出TRACE_TRANSCODING_REQUESTED的欄位會以表格中所示的順序顯示，並以索引標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| ad_id | 字串 | 完整廣告ID |
| ad_manifest_url | 字串 | 廣告資訊清單檔案的URL，來自廣告伺服器回應 |
| creative_type | 字串 | 媒體型別 |
| 標幟 | 字串 | ID3指出轉碼請求是否包含新增ID3標籤的請求 |
| target_duration | 字串 | 轉碼創意的目標持續時間（秒） |

### TRACE_TRACKING_REQUEST記錄 {#trace-tracking-request-records}

此型別的記錄表示執行伺服器端追蹤的請求。 超出TRACE_TRACKING_REQUEST的欄位會以表格中所示的順序顯示，並以索引標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| tracking_url_count | 整數 | 追蹤URL |
| 開始 | 浮點數 | PTS片段開始時間（以毫秒為精確度計算，以秒為單位） |
| 結束 | 浮點數 | PTS片段結束時間（以毫秒為精確度計算，以秒為單位） |

### TRACE_TRACKING_REQUEST_URL記錄 {#trace-tracking-request-url-records}

此型別的記錄會提供伺服器端追蹤的追蹤URL。 超出TRACE_TRACKING_REQUEST_URL的欄位會以表格中的順序顯示，並以索引標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| timestamp | 浮點數 | 在播放工作階段內偵測追蹤URL的時間（秒，精確度為。001） |
| ad_system | 字串 | 廣告系統（例如auditude） |
| url | 字串 | 要偵測的URL |

### TRACE_WEBVTT_REQUEST記錄 {#trace-webvtt-request-records}

此記錄型別的記錄要求資訊清單伺服器製作WEBVTT註解。 超出TRACE_WEBVTT_REQUEST的欄位會以表格中的順序顯示，並以索引標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| vtt_uri | 字串 | 請求的URL |
| 開始 | 浮點數 | 分割開始時間（以毫秒精確度計算，以秒為單位） |
| 結束 | 浮點數 | 分割結束時間（以毫秒精確度計算，以秒為單位） |

### TRACE_WEBVTT_RESPONSE記錄 {#trace-webvtt-response-records}

記錄 ``of ``此 ``type ``記錄 ``responses ``此 ``manifest ``伺服器 ``sends ``至 ``clients ``在 `` `answer` ``至 ``requests `` `for` ``WEBVTT ``註解。 TRACE_WEBVTT_RESPONSE以外的欄位會以表格中顯示的順序顯示，並以分隔符號分隔 `by`索引標籤。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| 回應 | 字串 | 傳送至使用者端的Base64編碼回應 |

### TRACE_WEBVTT_SOURCE記錄 {#trace-webvtt-source-records}

此型別的記錄會回應資訊清單伺服器對WEBVTT註解發出的要求。 超出TRACE_WEBVTT_SOURCE的欄位會以表格中所示的順序顯示，並以索引標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | 傳回HTTP狀態代碼 |
| source | 字串 | Base64編碼原始VTT內容 |


### TRACE_MISC記錄 {#trace-misc-records}

此型別的記錄可讓資訊清單伺服器記錄事件和資訊，而這些資訊不是為擷取廣告而計畫的。 TRACE_MISC以外的欄位包含訊息字串。 可能顯示的訊息包括：

* 已忽略的廣告：AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*， durationSeconds=*秒*，忽略=*忽略*，redirectAd=*redirectadad*，優先順序=*優先順序*
* 廣告放置傳回null。
* 廣告已成功拼接。
* 廣告呼叫失敗： *錯誤訊息*.
* 正在新增使用者代理程式以擷取原始資訊清單： *user-agent*.
* 新增Cookie以擷取原始資訊清單： [Cookie]
* 錯誤的URL *請求的URL錯誤訊息*. （無法剖析變體URL）
* 呼叫的URL： URL *Got return： response code*. （即時URL）
* 呼叫的URL： URL *傳回碼：回應碼*. ( VOD URL)
* 解決廣告時發現衝突：其中一個 — 中段開始或中段結束落在中段(VOD)中包含的前段或前段。
* 偵測到URI的處理常式擲回未處理的例外狀況： *請求URL*.
* 完成產生變體資訊清單。 （變體）
* 完成產生變體資訊清單。
* 處理VAST重新導向*重新導向URL *錯誤時發生例外狀況： *錯誤訊息*.
* 無法擷取廣告的播放清單 *廣告資訊清單URL*.
* 無法產生目標資訊清單。 (HLSManifestResolver)
* 無法剖析第一個廣告呼叫回應： *錯誤訊息*.
* 無法處理路徑的*GET|POST*要求： *請求URL*. （即時/VOD）
* 無法處理即時資訊清單要求： *請求URL*. （即時）
* 無法傳回變體資訊清單： *錯誤訊息*.
* 無法驗證群組ID： *群組識別碼*.
* 正在擷取原始資訊清單： *內容URL*. （即時）
* 下列VAST重新導向： *重新導向URL*.
* 找到空的可用性。 (VOD)
* 找到*number *ads。 (VOD)
* 已收到HTTP要求。 （第一則訊息）
* 略過廣告，因為廣告回應持續時間（*廣告回應持續時間*秒）與實際廣告持續時間（*實際持續時間*秒）之間的差異大於限制。 (HLSManifestResolver)
* 忽略未提供ID值的可用性。 (GroupAdResolver.java)
* 忽略提供無效時間值的可用性： *time *for availId = *可用ID*.
* 忽略提供無效持續時間值的可用性： *duration *若為availId = *可用ID*.
* 初始化新工作階段。 （變體）
* 無效的HTTP方法。 它必須是GET。 (VOD)
* 無效的HTTP方法。 追蹤要求必須是GET。 （即時）
* 無效的URL *請求的URL錯誤訊息*. （變體）
* 無效的群組。 (HLSManifestResolver)
* 無效的請求。 註解不是有效的追蹤要求。 (VOD)
* 無效的請求。 註解請求必須在工作階段建立後發出。 (VOD)
* 無效的請求。 追蹤要求必須在工作階段建立後提出。 (VOD)
* 多載群組ID的伺服器執行個體無效： *群組識別碼*. （即時）
* 已達到VAST重新導向限制 —  *數字*.
* 進行廣告呼叫： *廣告呼叫URL*.
* 找不到下列專案的資訊清單： *內容URL*. （即時）
* 找不到可用ID的相符可用性： *可用ID*. (HLSManifestResolver)
* 找不到播放工作階段。 (HLSManifestResolver)
* 正在處理資訊清單的VOD請求 *內容URL*.
* 正在處理變體。
* 正在處理資訊清單的標題要求 *內容URL*.
* 正在處理追蹤要求。 (VOD)
* 重新導向廣告回應為空白。 ( VASTStAX)
* 請求： *URL*.
* 傳回GET要求的錯誤回應，因為找不到播放工作階段。 (VOD)
* 因內部伺服器錯誤而傳回GET要求的錯誤回應。
* 針對指定無效資產的GET請求傳回錯誤回應： *廣告請求ID*. (VOD)
* 針對指定無效或空白群組ID的GET要求傳回錯誤回應： *群組識別碼*. (VOD)
* 針對指定無效追蹤位置值的GET要求傳回錯誤回應。 (VOD)
* 使用無效語法傳回GET請求的錯誤回應 —  *請求URL*. （即時/VOD）
* 使用不支援的HTTP方法傳回要求的錯誤回應： *GET|POST*. （即時/VOD）
* 正在從快取傳回資訊清單。 (VOD)
* 伺服器超載。 繼續進行而不需廣告拼接請求。 （變體）
* 開始產生目標資訊清單。 (HLSManifestResolver)
* 開始從下列來源產生變體資訊清單： *內容URL*. （變體）
* 開始將廣告拼接至資訊清單。 (VODHLSResolver)
* 嘗試拼接廣告 `HH:MM:SS`：AdPlacement \[adManifestURL=*廣告資訊清單URL*， durationSeconds=*秒*，忽略=*忽略*，redirectAd=*重新導向廣告*，優先順序=*優先順序*.\]
* 因為無效的時間軸而無法取得廣告 — 傳回了沒有廣告的內容。 (VOD)
* 無法取得廣告 — 傳回不含廣告的內容。 (VOD)
* 無法取得廣告查詢，且未提供內容URL。 (VOD)
* 收到有效的URL。 （VOD/變體）
* 找不到變體M3U8。 （變體）

### TRACE_追蹤_URL記錄 {#trace-tracking-url-records-1}

資訊清單伺服器會在伺服器端追蹤工作流程期間呼叫追蹤URL後，產生此類記錄。 TRACE_TRACKING_URL以外的欄位會以表格中顯示的順序顯示，並以索引標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 分 | 數字 | 串流中的PTS時間 |
| ad_system | 字串 | 廣告的廣告系統（auditude或freewheel） |
| url | 字串 | 已釘選的URL |
| state | 字串 | HTTP狀態代碼 |

### TRACE_播放_進度記錄 {#trace-playback-progress-records}

資訊清單伺服器會在伺服器端追蹤工作流程期間收到有關播放進度的訊號時，產生此類記錄。 TRACE_PLAYBACK_PROGRESS以外的欄位會以表格中顯示的順序顯示，並以標籤分隔。

| 欄位 | 型別 | 說明 |
|--- |--- |--- |
| 狀態 | 字串 | HTTP狀態代碼 |
| 頻寬 | 整數 | 串流的頻寬 |
| 分 | 整數 | 串流中的PTS時間 |
| ms_time | 整數 | 資訊清單伺服器產生追蹤URL的時間 |
| url | 字串 | 重新導向URL |
| header_user_agent | 字串 | HTTP User-Agent標頭 |
| header_dnt | 整數 | HTTP do-not-track標頭 |
| effective_remote_address | 字串 | IPv4有效的遠端位址 |
| remote_address | 字串 | Ipv4遠端位址 |

>[!NOTE]
>
>最後四個欄位是選用欄位。

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html) 頁面。
