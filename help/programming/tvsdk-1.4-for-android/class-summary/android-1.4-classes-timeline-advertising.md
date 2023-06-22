---
description: 這些類別會提供發生在時間軸內之廣告的相關資訊。
title: 時間表廣告類別
exl-id: fb31a235-6578-4da1-b732-713a2f9b24be
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# 時間表廣告類別{#timeline-advertising-classes}

這些類別會提供發生在時間軸內之廣告的相關資訊。

封裝： [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

封裝： [com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| 名稱 | 說明 |
|--- |--- |
| [廣告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 定義廣告抽象並保留所有廣告資訊的類別。 它由唯一ID、持續時間和 `MediaResource`. 此 `MediaResource` 包含實際廣告內容所在的URL。 |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 代表要顯示之資產的類別。 代表廣告資產的類別。 |
| [廣告插播](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 在播放期間某個時間點播放的數個廣告上提供統一檢視的類別。 |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | 廣告插播位置作業類別。 |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | 定義與搜尋時略過廣告的使用者相關之廣告播放原則的列舉。 |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 代表與資產相關聯之點選例項的類別。 此執行個體包含點進URL和標題的相關資訊，可用於向使用者提供其他資訊。 |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | 定義AdPolicySelector API呼叫屬性的介面。 這些屬性提供強制實行每個廣告行為的內容。 |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | 用於強制實施廣告行為的廣告原則選擇器介面。 應用程式可以透過實作所有必要的方法或擴充現有的預設原則選取器類別來自訂特定行為，來符合此介面。 |
| `auditude.AuditudeAdProvider` | 已棄用。 使用AuditudeResolver。 |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | 處理片語程式中的primetime和解析的類別。 |
| [Auditudetracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | 實作ContentTracker介面並定義Primetime廣告追蹤事件的類別。 |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | 處理片語處理中廣告解析部分的類別。 |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | 定義您必須實作通訊協定的介面，用來建立與資料庫或自訂廣告追蹤器整合的廣告追蹤模組。 此介面需要您定義向遠端廣告追蹤系統報告廣告進度事件的方式。 |
| [位置資訊](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | 抽象位置資訊請求的類別。 每個已解析廣告都必須附加一個版位資訊。 位置資訊說明廣告在時間軸上的放置位置。 其中包含下列資訊： <ul><li>位置位置（以毫秒為單位） </li><li>位置型別（前段、中段或後段） </li><li>即將取代之主要內容區塊的持續時間</li></ul> |
