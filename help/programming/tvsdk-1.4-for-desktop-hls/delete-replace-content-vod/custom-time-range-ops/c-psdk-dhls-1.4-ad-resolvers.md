---
description: 'null'
seo-description: 'null'
seo-title: 廣告解析器
title: 廣告解析器
uuid: 705df232-4adc-4f3a-b4aa-dafbd2b8fe4c
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 廣告解析器 {#ad-resolvers}

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
