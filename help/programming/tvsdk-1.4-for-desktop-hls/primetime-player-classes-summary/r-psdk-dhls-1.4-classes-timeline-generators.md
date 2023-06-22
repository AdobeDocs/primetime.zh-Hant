---
description: 這些類別有助於在時間軸中偵測投放內容（例如廣告）的機會。
title: 時間表產生器類別
exl-id: 2c9d1f10-fdf6-48b9-8bda-cee291befeab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 時間表產生器類別{#timeline-generators-classes}

這些類別有助於在時間軸中偵測投放內容（例如廣告）的機會。

封裝： [com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| 名稱 | 說明 |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | 為指定的廣告訊號模式建立初始機會的類別。 |
| [機會產生器](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | 所有機會產生器的基底類別。 |
| [OpportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | 機會產生器用來與TVSDK元件通訊的介面。 |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | 監視播放時間表並偵測插入資訊清單中做為SpliceOut註解的廣告放置商機的類別。 |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | 使用計時中繼資料資訊來偵測及產生廣告機會的機會產生器的預設實作。 |
