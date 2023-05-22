---
description: 這些類提供關於時間線內發生的廣告的資訊。
title: 時間軸廣告類
exl-id: 2ac1f6b7-48b2-4d9c-b39d-a7e6f1ff2ac5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 時間軸廣告類 {#timeline-advertising-classes}

這些類提供關於時間線內發生的廣告的資訊。

包： [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
包： [com.adobe.mediacore.timeline.adversition.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| 名稱 | 說明 |
|---|---|
| [廣告](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 定義Ad抽象並包含所有Ad資訊的類。 它由唯一ID、持續時間和 `MediaResource`。 的 `MediaResource` 包含實際廣告內容所在的URL。 |
| [廣告資產](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 表示要顯示的資產的類。 表示廣告資產的類。 |
| [廣告中斷](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 在播放期間某個時刻將播放的多個廣告提供統一視圖的類。 |
| [AdBreak策略](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | 定義與用戶相關的廣告播放策略的枚舉，該策略在查找時繞過廣告。 |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | 與特定廣告分段關聯的時間線項。 |
| [AdBreakStatedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | 何時將廣告中斷標籤為已監視的可能策略的枚舉類。 |
| [廣告點擊](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 表示與資產關聯的按一下實例的類。 此實例包含有關點擊式URL和標題的資訊，這些資訊可用於向用戶提供附加資訊。 |
| [廣告策略](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | 查找或特技播放模式後，在何處繼續播放廣告中斷的可能策略的枚舉類。 |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | 枚舉類，它列出播放器的播放方式，如查找或正常播放。 |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 定義屬性的介面 `AdPolicySelector` API調用。 這些屬性提供了強制執行每個廣告行為的上下文。 |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 用於強制廣告行為的廣告策略選擇器介面。 應用程式可以通過實施所有必需的方法或通過擴展現有預設策略選擇器類來自定義特定行為來遵循此介面。 |
| [AdTimeline項](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | 與特定廣告關聯的時間軸項。 |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | 在TVSDK進程中處理黃金時段廣告解析的類。 |
| [廣告類型](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | TVSDK支援的所有廣告類型的枚舉。 |
| [元資料AdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | 課。 |
