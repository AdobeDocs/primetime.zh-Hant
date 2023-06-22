---
description: 您可以使用回撥函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
title: 實作自訂中繼資料支援
exl-id: c7478578-7f49-4fd0-b381-c558888401aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 實作自訂中繼資料支援{#implement-custom-metadata-support}

您可以使用回撥函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。

回呼函式會在進行追蹤呼叫之前叫用，因此您的應用程式可以附加廣告或章節專屬的中繼資料。

為內容、廣告和章節叫用回呼函式。

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
