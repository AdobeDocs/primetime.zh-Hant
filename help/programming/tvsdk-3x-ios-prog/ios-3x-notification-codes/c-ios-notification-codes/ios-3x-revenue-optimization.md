---
description: '此表格提供「收入最佳化」通知的詳細資訊。 '
seo-description: '此表格提供「收入最佳化」通知的詳細資訊。 '
seo-title: 收入最佳化程式碼
title: 收入最佳化程式碼
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# 收入最佳化程式碼 {#revenue-optimization-code}

此表格提供有關收入最佳化通知的詳細資訊。

## 啟用收入最佳化報表 {#enable-revenue-optimization-reporting}

若要啟用此報表，請使用PTMediaPlayer api: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>大部分資訊性通知都包含相關的中繼資料，例如無法下載的資源URL。 有些通知包含中繼資料，以指定問題是發生在主要視訊內容、替代音訊內容或廣告中。

程式碼 |名稱 |內部通知 |中繼資料索引鍵 |注釋 |
|—|—|—|—|
|401001 | REVENUE_OPTIMIZATION_REPORTING |無 |請參閱下表，以瞭解根據不同事件的中繼資料索引鍵。 |無 |

| 事件詳細資料 | ContextMetadata |
|---|---|
| **在呼叫MediaPlayer::replaceCurrentResource時，在TVSDK中傳送CONTENT_RESOURCE_START** 。 | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePrequestTimeout, adRequestTimeout, adAdAdAdAdT, resourceTypeLoading, res, readLaing, creativeRepackagingEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** 當內容已進入準備狀態並準備好播放時，在TVSDK中傳送。 此事件不會在每次資訊清單上傳時派單——只會在初始載入時派單。 | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** Dissted in TVSDK when a opportunity is generated. | clientTimestamp, event, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_START** Disted in TVSDK（當業務機會開始解析時）。 | clientTimestamp, event, opportunityId, placementDuration, clientId |
| **當廣告解析程式呼叫MediaPlayerClient::notifyFailed()時，AD_OPPORTUNITY_RESOLVE_FAILED** 在TVSDK中傳送。 需要填寫資料 | opportunityId, notificationAD |
| **AD_RESOURCE_LOAD** 當URL擷取任何廣告資源時傳送。 responseStartTime：請求首次啟動時的Unix時間戳記。 responseTotalTime：回應載入所花費的總時間（以秒為單位）。 responseStatus：擷取資源時遇到的狀態代碼。 status:&quot;error&quot;或&quot;success&quot; referrerAdId：要求擷取此資源的反向連結廣告ID（如果存在）。 referrerUrl：要求擷取此資源的反向連結URL。 errorMessage：如果狀態為「error」，錯誤的原因將位於此處。 | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** 在TVSDK中將CRS套用至資產時傳送，以及m3u8的回應。 resourceType:always &quot;crs&quot;。 responseStartTime：請求首次啟動時的Unix時間戳記。 responseTotalTime：回應載入所花費的總時間（以秒為單位）。 responseStatus：擷取資源時遇到的狀態代碼。 狀態：「error」或「success」。 errorMessage：如果狀態為「error」，錯誤的原因將位於此處。 mediaFileUrl：選取的原始媒體檔案URL。 mediaFileBitrate：所選媒體檔案的位元速率。 mediaFileMimeType:所選媒體檔案的MIME類型。 url：最終資產URL。 | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **將adBreak置入時間軸後** ，在TVSDK中傳送AD_TIMELINE_PLACE。 每個廣告插播都會發生一次事件。 procedTime：請求放置廣告分段的時間。 actualTime：廣告插播的實際放置時間。 portedDuration：要求插入的廣告分段的持續時間。 對於即時內容，這會是提示持續時間。 對於VOD內容，這通常為-1。 actualDuration：插入廣告分段的實際持續時間。 計算為在原始串流時間軸中新增或取代的所有廣告的總持續時間（由其各自的區段持續時間定義）。 建議的廣告：建議廣告分段中的廣告數。 totalAds：成功放置的廣告數。 廣告……n：成功插入廣告將插入此處。 可從AD_OPPORTUNITY_RESOLVE_PROCESS檢索整個廣告清單資訊 | opportunityId, status, errorMessage, postedTime, postedDuration, actualTime, actualDuration, poustedAds, totalAds, ads_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_START** 在廣告開始播放後在TVSDK中傳送。 | clientTimestamp，事件， id, url, duration，類型， opportunityId, clientId |
| **廣告播放完成後** ，在TVSDK中傳送AD_PLAYBACK_COMPLETE。 | clientTimestamp，事件， id, url, duration，類型， opportunityId, clientId |
| **當adbreak開始播放時** ,TVSDK中的ADBREAK_PLAYBACK_START已傳送。 | clientTimestamp, event, opportunityId, duration，時間， clientId |
| **ADBREAK_PLAYBACK_COMPLETE** 在adbreak完成播放時在TVSDK中傳送。 | clientTimestamp, event, opportunityId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** 當任何內容完成時，在TVSDK中傳送。如果取代串流、播放器進入錯誤狀態、播放器重設或內容實際完成，則可能會發生此情況。 必須有此事件才能追蹤sessionId。 | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_ERROR** 當廣告播放時發生錯誤（變型串流錯誤）時，在TVSDK中傳送。 | event, error, timestamp, manifestUrl, time, opportunityId, url |