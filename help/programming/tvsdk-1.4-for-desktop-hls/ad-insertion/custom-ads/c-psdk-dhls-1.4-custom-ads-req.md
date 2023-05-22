---
description: 視頻播放器廣告服務介面定義(VPAID)提供了播放視頻廣告的通用介面。 VPAID為用戶提供豐富的媒體體驗，使出版商能夠更好地定位廣告、跟蹤廣告觀點和將視頻內容貨幣化。
title: 自定義廣告要求
exl-id: c13748d6-23f1-4f34-95b4-7b532db6e536
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 自定義廣告要求 {#custom-ad-requirements}

TVSDK播放器可以播放數字視頻播放器廣告介面定義(VPAID)廣告並顯示廣告載入狀態。 如果廣告中有錯誤或廣告載入時間過長，TVSDK將忽略這些廣告。

視頻播放器廣告服務介面定義(VPAID)提供了播放視頻廣告的通用介面。 VPAID為用戶提供豐富的媒體體驗，使出版商能夠更好地定位廣告、跟蹤廣告觀點和將視頻內容貨幣化。

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK支援以下功能：

* VPAID規範的1.0和2.0版
* 視頻點播(VOD)內容上的線性VPAID廣告
* FlashVPAID廣告

   VPAID廣告必須基於Flash，廣告響應必須將VPAID廣告的媒體類型標識為 `application/x-shockwave-flash`。

不支援以下功能：

* 諸如覆蓋廣告和動態伴生廣告等非線性廣告
* 預載入VPAID廣告
* 即時內容中的VPAID廣告
* JavaScript VPAID廣告

## 載入狀態 {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK派發以下事件：

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

在 `AdStopped` 事件，TVSDK將恢復視頻內容。

>[!TIP]
>
>如果指定零值，則TVSDK會嘗試載入廣告，直到它載入或出現錯誤。

## 忽略廣告 {#section_3EA452F420884335AE90DF23C17E416A}

如果載入廣告花費太長時間，或者廣告中有錯誤，TVSDK可以忽略該廣告，並自動播放廣告中的下一個廣告。

如果 `AuditudeSettings.customAdLoadTimeout` 設定指定大於零的秒數，TVSDK會嘗試將廣告載入到指定的持續時間。 如果無法載入廣告，則跳過廣告。 例如，如果配置 `AuditudeSettings.customAdLoadTimeout:5`, TVSDK將嘗試載入廣告最多5秒。 如果廣告仍未載入，則忽略該廣告。
