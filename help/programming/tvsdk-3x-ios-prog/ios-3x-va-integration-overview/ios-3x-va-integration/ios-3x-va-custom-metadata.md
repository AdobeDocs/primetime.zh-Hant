---
description: 您可以使用回調函式提供有關內容、廣告和章節跟蹤調用的自定義元資料。
title: 實施自定義元資料支援
exl-id: d5d8b476-0f7c-434c-9386-d060a6eb99f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 實施自定義元資料支援 {#implement-custom-metadata-support}

您可以使用回調函式提供有關內容、廣告和章節跟蹤調用的自定義元資料。

回調函式在進行跟蹤調用之前即被調用，因此您的應用程式可以附加特定於廣告或章節的元資料。

1. 調用內容、廣告和章節的回調函式。

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
