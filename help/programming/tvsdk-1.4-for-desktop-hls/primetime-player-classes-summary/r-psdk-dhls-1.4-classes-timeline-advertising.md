---
description: 這些類別會提供發生在時間軸內之廣告的相關資訊。
title: 時間表廣告類別
exl-id: 2ac1f6b7-48b2-4d9c-b39d-a7e6f1ff2ac5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 時間表廣告類別 {#timeline-advertising-classes}

這些類別會提供發生在時間軸內之廣告的相關資訊。

封裝： [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
封裝： [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| 名稱 | 說明 |
|---|---|
| [廣告](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 定義廣告抽象並保留所有廣告資訊的類別。 它由唯一ID、持續時間和 `MediaResource`. 此 `MediaResource` 包含實際廣告內容所在的URL。 |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 代表要顯示之資產的類別。 代表廣告資產的類別。 |
| [廣告插播](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 在播放期間某個時間點播放的數個廣告上提供統一檢視的類別。 |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | 定義與搜尋時略過廣告的使用者相關之廣告播放原則的列舉。 |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | 與特定廣告插播相關聯的時間軸專案。 |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | 何時將廣告插播標示為已觀看的可能原則的列舉類別。 |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 代表與資產相關聯之點選例項的類別。 此執行個體包含點進URL和標題的相關資訊，可用於向使用者提供其他資訊。 |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | 列舉類別，瞭解在搜尋或特技播放模式後，從何處繼續播放廣告插播的可能原則。 |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | 列舉類別，列出播放器播放的方式，例如搜尋或正常播放。 |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 定義屬性的介面 `AdPolicySelector` API呼叫。 這些屬性提供強制實行每個廣告行為的內容。 |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 用於強制實施廣告行為的廣告原則選擇器介面。 應用程式可以透過實作所有必要的方法或擴充現有的預設原則選取器類別來自訂特定行為，來符合此介面。 |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | 與特定廣告關聯的時間軸專案。 |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | 在TVSDK程式中處理primetime廣告解析的類別。 |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | TVSDK支援的所有廣告型別列舉。 |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | 類別。 |
