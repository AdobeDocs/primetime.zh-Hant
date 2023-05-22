---
description: 下表提供了有關收入優化通知的詳細資訊。
title: 收入優化代碼
exl-id: 3657ba70-ec35-495b-ae7b-4198429bdf6a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# 收入優化代碼 {#revenue-optimization-code}

下表提供了有關REVENUE OPTIMIZATION通知的詳細資訊。

## 啟用收入優化報告 {#enable-revenue-optimization-reporting}

要啟用此報告，請使用PTMediaPlayer api: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`。

>[!NOTE]
>
>大多數資訊性通知都包含相關的元資料，例如，無法下載的資源的URL。 某些通知包含元資料，用於指定是在主視頻內容、備用音頻內容還是廣告中出現問題。

| 代碼 | 名稱 | 內部通知 | 元資料鍵 | 注釋 |
|---|---|---|---|---|
| 401001 | 收入_優化_報告 | 無 | 有關基於不同事件的元資料鍵，請參閱下表。 | 無 |

| 事件詳細資訊 | 上下文元資料 |
|---|---|
| **內容資源啟動** 調用MediaPlayer:replaceCurrentResource時在TVSDK中調度。 | clientTimestamp、fallbackOnInvalidCreative、showStaticBanners、hasPreroll、event、adSigningMode、resourceUrl、creativeRepackagingFormat、delayAdLoadingTolerance、zoneID、hasLivePreroll、adRequestTimeout、deaedAdAdAdAdLoad、remedRemet、remedReadReadReadedReadReadDRead、redDReadLedRedRedLe、redResedReadR、redRes、reloading、res、redResesedReseseseseReseRes、resourceRese, creativeRepackagingEnabled, mediaId, clientId |
| **內容回放開始** 當內容已進入準備狀態並準備好播放時，在TVSDK中調度。 此事件不會在每個清單上載上發送 — 只會在初始負載上發送。 | clientTimestamp、contentURL、contentType、event、isLive、clientID |
| **AD_OPPORTUNITY_GENERATED** 在生成機會時在TVSDK中調度。 | clientTimestamp、event、opportunityId、placementDuration、clientId |
| **AD_OPPORTUNITY_RESOLVE_START** 當機會開始解決時，在TVSDK中派送。 | clientTimestamp、event、opportunityId、placementDuration、clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** 當廣告解析程式調用MediaPlayerClient::notifyFailed()時，在TVSDK中調度。 需要填充資料 | opportunityId,notificationAD |
| **AD_RESOURCE_LOAD** 當URL提取任何廣告資源時調度。 responseStartTime：請求首次啟動時的Unix時間戳。 responseTotalTime：響應負載所花費的總時間（秒）。 responseStatus：獲取資源時遇到的狀態代碼。 狀態：&quot;error&quot;或&quot;success&quot; referrerAdId：請求提取此資源的引用ad id（如果存在）。 referrerUrl：請求獲取此資源的引用URL。 錯誤消息：如果狀態為「error」，則錯誤原因將位於此處。 | opportunityId、resourceType、responseTotalTime、responseStatus、responseStartTime、status、errorMessage、url、referrerURL、referrerAdId |
| **AD_RESOURCE_LOAD_CRS** 在TVSDK中將CRS應用於資產時派送，以及m3u8的響應。 resourceType:always &quot;crs&quot;。 responseStartTime：請求首次啟動時的Unix時間戳。 responseTotalTime：響應負載所花費的總時間（秒）。 responseStatus：獲取資源時遇到的狀態代碼。 狀態：「error」或「success」。 錯誤消息：如果狀態為「error」，則錯誤原因將位於此處。 mediaFileUrl：選定的原始媒體檔案url。 mediaFileBitrate：所選媒體檔案的比特率。 mediaFileMimeType:選定的媒體檔案的mime類型。 url：最終資產url。 | opportunityId、resourceType、responseTotalTime、responseStatus、responseStartTime、status、errorMessage、url、mediaFileURL、mediaFileBitrate、mediaFileMimeType、url |
| **AD_TIMELINE_PLACE** 在時間線上放置adBreak後在TVSDK中調度。 每個廣告中斷都會發生一次事件。 prosedTime：請求放置廣告中斷的時間。 actualTime：廣告分段實際放置的時間。 prosedDuration：請求插入的廣告分段的持續時間。 對於即時內容，這將是提示持續時間。 對於VOD內容，通常為–1。 actualDuration：插入廣告分段的實際持續時間。 計算為在原始流時間線中添加或替換的所有廣告的總持續時間，由它們各自的段持續時間定義。 建議廣告：建議廣告分段中的廣告數。 totalAds：成功放置的廣告數。 廣告……n：成功插入廣告將插入此處。 可以從AD_OPPORTUNITY_RESOLVE_PROCESS檢索整個廣告清單資訊 | opportunityId、status、errorMessage、pussedTime、pussedDuration、actualTime、actualDuration、pussedAds、totalAds、adsid、adstype、adsduration、adsurl |
| **AD_PLAYBACK_START** 在廣告開始播放後在TVSDK中派送。 | clientTimestamp，事件， id, url，持續時間，類型， opportunityId, clientId |
| **AD_PLAYBACK_COMPLETE** 在廣告完成播放後在TVSDK中派送。 | clientTimestamp，事件， id, url，持續時間，類型， opportunityId, clientId |
| **ADBREAK_PLAYBACK_START** 在TVSDK中，當adbreak開始播放時派送。 | clientTimestamp，事件， opportunityId，持續時間，時間，clientId |
| **ADBREAK_PLAYBACK_COMPLETE** 在adbreak完成播放後在TVSDK中調度。 | clientTimestamp 、 event 、 opportunityId 、 clientId |
| **內容回放完成** 當任何內容完成時在TVSDK中調度。如果流被替換、播放器進入錯誤狀態、播放器被重置或內容實際完成，則可能會發生這種情況。 跟蹤sessionId時需要此事件。 | clientTimestamp，事件， clientId, url, status，錯誤消息 |
| **AD_PLAYBACK_ERROR** 當播放廣告時出錯（變型流錯誤），在TVSDK中調度。 | 事件，錯誤，時間戳， manifestUrl，時間， opportunityId, url |
