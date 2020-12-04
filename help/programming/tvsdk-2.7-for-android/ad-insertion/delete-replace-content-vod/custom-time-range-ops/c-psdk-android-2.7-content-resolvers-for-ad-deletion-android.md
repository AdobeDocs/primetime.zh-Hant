---
description: 您可以使用多個內容解析器來處理不同的時間軸操作。
seo-description: 您可以使用多個內容解析器來處理不同的時間軸操作。
seo-title: 廣告刪除／取代的內容解析器
title: 廣告刪除／取代的內容解析器
uuid: ed168c52-ab7b-4fe6-8775-eb18018dc249
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---


# 廣告刪除／取代的內容解析器{#content-resolvers-for-ad-deletion-replacement}

您可以使用多個內容解析器來處理不同的時間軸操作。

```java
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
    List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
    MediaPlayerItemConfig itemConfig = item.getConfig(); 
    if(itemConfig) { 
        CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
        if (customRanges) { 
            List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
 
            if (timeRanges && timeRanges.size() > 0) { 
                //CustomRangeResolver is activated by the presence of CustomRanges 
                resolvers.add(new CustomRangeResolver()); 
            } 
        } 
        AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
        if (metadata) { 
            if (metadata instanceOf AuditudeSettings)  
            resolvers.add(new AuditudeResolver(getContext());                                      
        } 
    } 
    //Add your custom resolver if any 
    resolvers.add(MyOpportunityGenerator(item)); 
    return resolvers; 
} 
```

