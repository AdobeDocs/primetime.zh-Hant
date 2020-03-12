---
description: 您可以使用TVSDK設定檔(AdobeTVSDKonfig.json)來更新VAST/VMAP回應廣告創意選擇的優先順序。 您也可以使用此設定檔案來定義廣告創作人員的來源URL轉換規則。
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: 您可以使用TVSDK設定檔(AdobeTVSDKonfig.json)來更新VAST/VMAP回應廣告創意選擇的優先順序。 您也可以使用此設定檔案來定義廣告創作人員的來源URL轉換規則。
seo-title: 更新廣告創意選擇規則
title: 更新廣告創意選擇規則
uuid: c33fe1f0-78cb-4dc2-89d2-e9fb1bf0e73f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 概觀 {#update-ad-creative-selection-rules-overview}

您可以使用TVSDK設定檔(AdobeTVSDKonfig.json)來更新VAST/VMAP回應廣告創意選擇的優先順序。 您也可以使用此設定檔案來定義廣告創作人員的來源URL轉換規則。

當您的視訊播放器向廣告伺服器提出要求時，VAST/VMAP回應通常會包含多個廣告創意素材( `MediaFile` 元素)，其中每個元素都會提供不同容器轉碼器版本的URL。 在某些情況下，VAST/VMAP回應中的廣告創意素材會為廣告提供不同的位元速率。 如果您想要為這些廣告創意人員指定自己的優先順序和轉換規則，可以在設定檔案中 [!DNL AdobeTVSDKConfig.json] 這麼做。

>[!IMPORTANT]
>
>* 請勿變更TVSDK設定檔的名稱。 名稱必須保留 [!DNL AdobeTVSDKConfig.json]。
>* 您可以將此檔案放置在您套件可存取的任何地方。
>



您可以在中指定兩種類型的規則 [!DNL AdobeTVSDKConfig.json]:優 *先順序**,* 標準化規則。

**[!UICONTROL Disabling Pre-Roll]**

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

要禁用即時流上的前滾，應該更改為僅包括SpliceOutOpportunityGenerator :

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

