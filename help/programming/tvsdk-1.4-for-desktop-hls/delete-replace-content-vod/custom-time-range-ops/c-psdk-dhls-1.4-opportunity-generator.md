---
title: 機會生成器
description: 機會生成器
copied-description: true
exl-id: ee8d239f-7c52-44ea-a238-cc46d46cf128
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '6'
ht-degree: 0%

---

# 機會生成器{#opportunity-generator}

```
if (resource.metadata != null) { 
 // push in the CustomRangeResolver before other resolvers 
    if (resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_DELETE_RANGES_METADATA_KEY) 
        result.push(new CustomRangeResolver()); 
    else if (resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_REPLACE_RANGES_METADATA_KEY)) 
        result.push(new CustomRangeResolver()); 
    if (resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY)) { 
        result.push(new CustomAdResolver());    // no ad insertion with mark ranges 
    } 
    else if (resource.metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY)) { 
        if (_auditudeResolver == null) { 
              _auditudeResolver = new AuditudeResolver(); 
        } 
        result.push(_auditudeResolver); 
    } 
    else if (resource.metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY)) { 
        result.push(new MetadataResolver()); 
    } 
}
```
