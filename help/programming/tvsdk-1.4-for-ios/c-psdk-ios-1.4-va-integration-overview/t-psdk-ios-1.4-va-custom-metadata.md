---
description: 您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
seo-description: 您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
seo-title: 實作自訂中繼資料支援
title: 實作自訂中繼資料支援
uuid: eb8d383f-a3e8-402d-84e8-f4209df0f954
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 實作自訂中繼資料支援{#implement-custom-metadata-support}

您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。

回呼函式會在進行追蹤呼叫之前呼叫，因此您的應用程式可以附加廣告或章節專屬的中繼資料。

叫用內容、廣告和章節的回呼函式。

```
// Video Metadata Block 
    vaTrackingMetadata.videoMetadataBlock = ^NSDictionary *() 
    { 
        return @{ 
                 @"myvideoid": @"1234", 
                 @"mysdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Ad Metadata Block invoked on every ad start 
    vaTrackingMetadata.adMetadataBlock = ^NSDictionary *(PTAd *ad) 
    { 
        return @{ 
                 @"myadid": @"ad-1234", 
                 @"myad-sdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Chapter Metadata Block invoked on every chapter start 
    vaTrackingMetadata.chapterMetadataBlock = ^NSDictionary *(PTVideoAnalyticsChapterData *chapter) 
    { 
        return @{ 
                 @"mychapterid": @"chapter-1234", 
                 @"mychapter-sdkversion": [PTSDK apiVersion] 
                 }; 
    };
```

