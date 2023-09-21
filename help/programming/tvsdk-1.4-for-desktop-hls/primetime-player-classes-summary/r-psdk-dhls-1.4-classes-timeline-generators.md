---
description: 這些類別有助於在時間軸中偵測刊登內容（例如廣告）的機會。
title: 時間表產生器類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 時間表產生器類別{#timeline-generators-classes}

這些類別有助於在時間軸中偵測刊登內容（例如廣告）的機會。

封裝： [com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| 名稱 | 說明 |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | 為指定的廣告訊號模式建立初始機會的類別。 |
| [OpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | 所有機會產生器的基底類別。 |
| [OpportunergeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | 機會產生器用來與TVSDK元件通訊的介面。 |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | 類別，可監視播放時間軸，並偵測插入資訊清單中做為SpliceOut註解的廣告置入機會。 |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | 機會產生器的預設實作，此產生器使用定時中繼資料資訊來偵測和產生廣告機會。 |
