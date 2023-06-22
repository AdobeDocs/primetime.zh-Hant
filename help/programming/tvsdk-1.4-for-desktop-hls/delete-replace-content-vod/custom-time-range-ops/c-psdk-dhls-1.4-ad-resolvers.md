---
title: 廣告解析程式
description: 廣告解析程式
copied-description: true
exl-id: 0df17e35-5c2d-46cd-bab2-c240ab8320c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '6'
ht-degree: 0%

---

# 廣告解析程式 {#ad-resolvers}

```
if (resource.metadata != null) { 
    if (resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_DELETE_RANGES_METADATA_KEY) 
            || resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_REPLACE_RANGES_METADATA_KEY) 
            || resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY)) 
    { 
        // Use the CustomRangesOpportunityGenerator for custom ranges opportunities 
        result.push(new CustomRangesOpportunityGenerator());  
        if (resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_DELETE_RANGES_METADATA_KEY))  { 
            result.push(new AdSignalingModeOpportunityGenerator());       
            // Manifest cue mode ignores replace range 
            result.push(new SpliceOutOpportunityGenerator()); 
        } 
        return result; 
    } 
}
```
