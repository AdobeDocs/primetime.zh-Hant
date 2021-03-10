---
description: 這些類別提供有關時間軸中發生廣告的資訊。
title: 時間軸廣告課程
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# 時間軸廣告類{#timeline-advertising-classes}

這些類別提供有關時間軸中發生廣告的資訊。

套件：[com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

套件：[com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| 名稱 | 說明 |
|--- |--- |
| [廣告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 定義廣告抽象並包含所有廣告資訊的類別。 它由唯一ID、持續時間和`MediaResource`定義。 `MediaResource`包含實際廣告內容所在的URL。 |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 表示要顯示的資產的分類。 代表廣告資產的分類。 |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 提供數個廣告統一檢視的類別，在播放期間的某個時間點播放。 |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | 廣告插播位置操作類。 |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | 定義與搜尋時略過廣告的使用者相關的廣告播放原則的列舉。 |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 表示與資產關聯之點按例項的分類。 此例項包含有關點進URL和標題的資訊，這些資訊可用來提供使用者其他資訊。 |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | 定義AdPolicySelector API呼叫屬性的介面。 這些屬性提供實施每個廣告行為的上下文。 |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | 用於強制廣告行為的廣告策略選擇器介面。 應用程式可實作所有必要方法，或擴充現有的預設原則選擇器類別以自訂特定行為，以符合此介面。 |
| `auditude.AuditudeAdProvider` | 已過時。 使用AuditudeResolver。 |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | 在片語處理中處理黃金時段廣告解析的類別。 |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | 實作ContentTracker介面並定義Primetime廣告追蹤事件的類別。 |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | 在片語處理中處理廣告解析部分的類。 |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | 定義您必須實作之通訊協定的介面，以建立廣告追蹤模組，以便與程式庫或自訂廣告追蹤器整合。 此介面要求您定義向遠端廣告追蹤系統報告廣告進度事件的方式。 |
| [位置資訊](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | 抽象位置資訊要求的類別。 每個已解決的廣告都必須附上一個位置資訊。 位置資訊說明廣告要放置在時間軸上的位置。 它包含以下資訊： <ul><li>位置（毫秒） </li><li>位置類型（前滾、中滾或後滾） </li><li>將要替換的主要內容塊的持續時間</li></ul> |
