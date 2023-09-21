---
title: 機會產生器
description: 機會產生器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6'
ht-degree: 0%

---

# 機會產生器{#opportunity-generator}

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
