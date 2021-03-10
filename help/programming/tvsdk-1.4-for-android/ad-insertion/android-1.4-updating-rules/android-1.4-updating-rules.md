---
description: 您可以使用TVSDK設定檔(AdobeTVSDKonfig.json)來更新VAST/VMAP回應廣告創意選擇的優先順序。 您也可以使用此設定檔案來定義廣告創作人員的來源URL轉換規則。
keywords: 創意選擇規則；AdobeTVSDKonfig；廣告創意優先順序；轉換規則
title: 更新廣告創意選擇規則
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 概述{#updating-ad-creative-selection-rules-overview}

您可以使用TVSDK設定檔(AdobeTVSDKonfig.json)來更新VAST/VMAP回應廣告創意選擇的優先順序。 您也可以使用此設定檔案來定義廣告創作人員的來源URL轉換規則。

當您的視訊播放器向廣告伺服器提出要求時，VAST/VMAP回應通常包含多個廣告創意素材（`MediaFile`元素），每個元素都會提供不同容器轉碼器版本的URL。 在某些情況下，VAST/VMAP回應中的廣告創意素材會為廣告提供不同的位元速率。 如果您想要為這些廣告創作元素指定自己的優先順序和轉換規則，可以在[!DNL AdobeTVSDKConfig.json]組態檔中指定。

>[!IMPORTANT]
>
>* 請勿變更TVSDK設定檔的名稱。 名稱必須保留[!DNL AdobeTVSDKConfig.json]。
>* 此檔案必須放在項目的[!DNL assets/]資料夾中。

>



您可以在[!DNL AdobeTVSDKConfig.json]中指定兩種規則類型：*優先順序*&#x200B;規則和&#x200B;*標準化*&#x200B;規則。

## 禁用前滾{#disabling-preroll}

要禁用前滾，您需要更改預設的機會生成器以不進行前滾呼叫。 依預設，TVSDK會使用下列商機產生器：

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    result.push(new AdSignalingModeOpportunityGenerator()); 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
} 
```

要禁用即時流上的前滾，應將其更改為僅包括SpliceOutOpportunityGenerator:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    if (preroll_enabled == true) { 
        result.push(new AdSignalingModeOpportunityGenerator()); 
    } 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
}
```

