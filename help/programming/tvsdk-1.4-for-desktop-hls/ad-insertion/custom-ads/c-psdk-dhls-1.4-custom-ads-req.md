---
description: 影片播放器廣告服務介面定義(VPAID)提供播放影片廣告的通用介面。 VPAID為使用者提供豐富的媒體體驗，並使得發佈者能更妥善地鎖定廣告、追蹤廣告印象，以及從視訊內容獲利。
title: 自訂廣告需求
exl-id: c13748d6-23f1-4f34-95b4-7b532db6e536
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 自訂廣告需求 {#custom-ad-requirements}

TVSDK播放器可以播放數位視訊播放器廣告介面定義(VPAID)廣告，並顯示廣告載入狀態。 如果廣告發生錯誤，或廣告載入時間過長，TVSDK會忽略這些廣告。

影片播放器廣告服務介面定義(VPAID)提供播放影片廣告的通用介面。 VPAID為使用者提供豐富的媒體體驗，並使得發佈者能更妥善地鎖定廣告、追蹤廣告印象，以及從視訊內容獲利。

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK支援下列功能：

* VPAID規格的1.0版和2.0版
* 線性VPAID隨選影片(VOD)內容廣告
* FlashVPAID廣告

   VPAID廣告必須以Flash為基礎，廣告回應必須將VPAID廣告的媒體型別識別為 `application/x-shockwave-flash`.

不支援下列功能：

* 非線性廣告，例如覆蓋廣告和動態隨附廣告
* 預先載入VPAID廣告
* 即時內容中的VPAID廣告
* JavaScript VPAID廣告

## 正在載入狀態 {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK會傳送以下事件：

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

晚於 `AdStopped` 事件， TVSDK會繼續播放視訊內容。

>[!TIP]
>
>如果您指定零值，TVSDK會嘗試載入廣告，直到載入或發生錯誤為止。

## 忽略廣告 {#section_3EA452F420884335AE90DF23C17E416A}

如果廣告載入時間過長或廣告中發生錯誤，TVSDK可以忽略廣告，且廣告Pod中的下一個廣告會自動播放。

如果 `AuditudeSettings.customAdLoadTimeout` 設定會指定大於零的秒數，TVSDK會嘗試將廣告載入指定的持續時間。 如果無法載入廣告，則會略過廣告。 例如，如果您設定 `AuditudeSettings.customAdLoadTimeout:5`，TVSDK會嘗試載入廣告最多5秒。 如果廣告仍未載入，則會被忽略。
