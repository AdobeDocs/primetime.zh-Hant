---
description: 這些類提供關於時間線內發生的廣告的資訊。
title: 時間軸廣告類
exl-id: fb31a235-6578-4da1-b732-713a2f9b24be
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# 時間軸廣告類{#timeline-advertising-classes}

這些類提供關於時間線內發生的廣告的資訊。

包： [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

包： [com.adobe.mediacore.timeline.advertising.audited](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| 名稱 | 說明 |
|--- |--- |
| [廣告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 定義Ad抽象並包含所有Ad資訊的類。 它由唯一ID、持續時間和 `MediaResource`。 的 `MediaResource` 包含實際廣告內容所在的URL。 |
| [廣告資產](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 表示要顯示的資產的類。 表示廣告資產的類。 |
| [廣告中斷](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 在播放期間某個時刻將播放的多個廣告提供統一視圖的類。 |
| [廣告中斷放置](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | 廣告中斷放置操作類。 |
| [AdBreak策略](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | 定義與用戶相關的廣告播放策略的枚舉，該策略在查找時繞過廣告。 |
| [廣告點擊](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 表示與資產關聯的按一下實例的類。 此實例包含有關點擊式URL和標題的資訊，這些資訊可用於向用戶提供附加資訊。 |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | 定義AdPolicySelector API調用屬性的介面。 這些屬性提供了強制執行每個廣告行為的上下文。 |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | 用於強制廣告行為的廣告策略選擇器介面。 應用程式可以通過實施所有必需的方法或通過擴展現有預設策略選擇器類來自定義特定行為來遵循此介面。 |
| `auditude.AuditudeAdProvider` | 已棄用。 使用AuditudeResolver。 |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | 在短語流程中處理黃金時段廣告解析的類。 |
| [奧迪跟蹤器](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | 實現ContentTracker介面並定義Mighide廣告跟蹤事件的類。 |
| [內容解析器](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | 處理短語進程中廣告解析部分的類。 |
| [內容跟蹤器](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | 用於定義要建立廣告跟蹤模組以與庫或自定義廣告跟蹤器整合時必須實現的協定的介面。 此介面要求您定義向遠程廣告跟蹤系統報告廣告進度事件的方式。 |
| [放置資訊](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | 抽取放置資訊請求的類。 每個已解析的廣告必須附加一個放置資訊。 該放置資訊描述了廣告要放置在時間軸上的位置。 它包含以下資訊： <ul><li>位置（毫秒） </li><li>放置的類型（前滾、中滾或後滾） </li><li>將要替換的主內容塊的持續時間</li></ul> |
