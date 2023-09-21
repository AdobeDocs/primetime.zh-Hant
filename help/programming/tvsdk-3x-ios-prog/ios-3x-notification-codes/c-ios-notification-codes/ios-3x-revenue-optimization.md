---
description: 此表格提供收入最佳化通知的詳細資訊。
title: 收入最佳化程式碼
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# 收入最佳化程式碼 {#revenue-optimization-code}

此表格提供有關「收入最佳化」通知的詳細資訊。

## 啟用收入最佳化報表 {#enable-revenue-optimization-reporting}

若要啟用此報表，請使用PTMediaPlayer api： `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>大多數資訊通知包含相關的中繼資料，例如，無法下載的資源的URL。 有些通知包含中繼資料，用於指定問題發生在主要視訊內容、替代音訊內容還是廣告中。

| 程式碼 | 名稱 | 內部通知 | 中繼資料索引鍵 | 註解 |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_REPORTING | 無 | 如需根據不同事件的中繼資料索引鍵，請參閱下表。 | 無 |

| 活動詳細資料 | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** 呼叫MediaPlayer：：replaceCurrentResource時在TVSDK中傳送。 | clientTimestamp， fallbackOnInvalidCreative， showStaticBanners， hasPreroll， event， adSignalingMode， resourceUrl， creativeRepackagingFormat， delayAdLoadingTolerance， zoneID， hasLivePreroll， adRequestTimeout， delayAdLoading， resourceType， creativeRepackagingEnabled， mediaId， cliged |
| **CONTENT_PLAYBACK_START** 當內容已進入準備狀態並準備好要播放時，在TVSDK中傳送。 此事件不會在每次資訊清單上傳時傳送 — 僅在初始載入時傳送。 | clientTimestamp， contentURL， contentType， event， isLive， clientID |
| **AD_OPPORTUNITY_GENERATED** 產生機會時在TVSDK中分派。 | clientTimestamp、event、opportunityId、placementDuration、clientId |
| **AD_OPPORTUNITY_RESOLVE_START** 當機會開始解析時在TVSDK中分派。 | clientTimestamp、event、opportunityId、placementDuration、clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** 當廣告解析程式呼叫MediaPlayerClient：：notifyFailed()時，在TVSDK中傳送。 需要填寫資料 | opportunityId， notificationAD |
| **AD_RESOURCE_LOAD** 當URL擷取任何廣告資源時傳送。 responseStartTime：要求首次啟動時的Unix時間戳記。 responseTotalTime：載入回應所花費的總時間（以秒為單位）。 responseStatus：擷取資源時遇到狀態代碼。 status：&quot;error&quot;或&quot;success&quot; referrerAdId：要求擷取此資源的反向連結廣告ID （如果存在）。 referrerUrl：要求擷取此資源的反向連結URL。 errorMessage：如果狀態為「error」，錯誤原因將位於此處。 | opportunityId， resourceType， responseTotalTime， responseStatus， responseStartTime， status， errorMessage， url， referrerURL， referrerAdId |
| **AD_RESOURCE_LOAD_CRS** 當CRS套用至資產以及m3u8的回應時，在TVSDK中傳送。 resourceType：一律為&quot;crs&quot;。 responseStartTime：要求首次啟動時的Unix時間戳記。 responseTotalTime：載入回應所花費的總時間（以秒為單位）。 responseStatus：擷取資源時遇到狀態代碼。 status：&quot;error&quot;或&quot;success&quot;。 errorMessage：如果狀態為「error」，錯誤原因將位於此處。 mediaFileUrl：選取的原始媒體檔案url。 mediaFileBitrate：所選取媒體檔案的位元速率。 mediaFileMimeType：選取之媒體檔案的mime型別。 url：最終資產url。 | opportunityId， resourceType， responseTotalTime， responseStatus， responseStartTime， status， errorMessage， url， mediaFileURL， mediaFileBitrate， mediaFileMimeType， url |
| **AD_TIMELINE_PLACE** 在時間軸上放置adBreak後，於TVSDK中傳送。 此事件將在每個廣告插播發生一次。 proposedTime：要求放置廣告插播的時間。 actualTime：廣告插播實際放置的時間。 proposedDuration：要求插入的廣告插播持續時間。 如果是即時內容，這會是提示持續時間。 若是VOD內容，該值通常為–1。 actualDuration：插入的廣告插播實際持續時間。 計算為在原始串流時間軸中新增或取代的所有廣告的總持續時間，由廣告的個別區段持續時間定義。 proposedAds：建議的廣告插播中的廣告數量。 totalAds：成功刊登的廣告數。 廣告……n：成功插入的廣告將會插入此處。 可從AD_OPPORTUNITY_RESOLVE_PROCESS擷取整個廣告資訊清單資訊 | opportunityId、status、errorMessage、proposedTime、proposedDuration、actualTime、actualDuration、proposedAds、totalAds、ads_id、ads_type、ads_duration、ads_url |
| **AD_PLAYBACK_START** 在廣告開始播放後於TVSDK中傳送。 | clientTimestamp、事件、id、url、持續時間、型別、opportunityId、clientId |
| **AD_PLAYBACK_COMPLETE** 在廣告完成播放後於TVSDK中傳送。 | clientTimestamp、事件、id、url、持續時間、型別、opportunityId、clientId |
| **ADBREAK_PLAYBACK_START** 在廣告插播開始播放時在TVSDK中傳送。 | clientTimestamp、event、opportunityId、duration、time、clientId |
| **ADBREAK_PLAYBACK_COMPLETE** 當廣告完成播放時，在TVSDK中傳送。 | clientTimestamp、event、opportunityId、clientId |
| **CONTENT_PLAYBACK_COMPLETE** 當任何內容完成時，會在TVSDK中傳送。如果資料流遭取代、播放器進入錯誤狀態、播放器遭重設，或內容實際完成，就可能發生這種情況。 追蹤sessionId需要此事件。 | clientTimestamp， event， clientId， url， status， errorMessage |
| **AD_PLAYBACK_ERROR** 當廣告播放時發生錯誤（變體資料流錯誤）時，在TVSDK中傳送。 | 事件，錯誤，時間戳記， manifestUrl，時間， opportunityId， url |
