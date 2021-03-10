---
title: 廣告解析器
description: 廣告解析器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '6'
ht-degree: 0%

---


# 廣告解析器{#ad-resolvers}

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
