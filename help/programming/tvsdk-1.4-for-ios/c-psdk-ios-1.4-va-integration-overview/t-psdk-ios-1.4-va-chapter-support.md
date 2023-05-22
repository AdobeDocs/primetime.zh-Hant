---
title: 實施章節支援
description: 實施章節支援
copied-description: true
exl-id: 4585505c-9511-4f10-b81a-922eaeb2764d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 實施章節支援{#implement-chapter-support}

您可以通過以下方式定義和跟蹤基於TVSDK的應用程式中視頻跟蹤的章節：

* 預設章節，由TVSDK內部管理。

   本章定義為每個廣告中斷之間的時間。 例如，預卷和中卷之間的時間定義為第一章。
* 自定義章節，這些章節由應用程式管理，並基於CMS資料或應用程式用於定義章節的其他方式。

   定義和跟蹤預設或自定義章節。

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaTrackingMetadata.enableChapterTracking = YES; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example, 3 chapters of 60 second duration each: 
   
       NSMutableArray *chapters = [[[NSMutableArray alloc] init] autorelease]; 
   
       int chapterDuration = 60; 
       for (int i = 0; i < 3; i++) 
       { 
           PTVideoAnalyticsChapterData *chapterData =  
             [[[PTVideoAnalyticsChapterData alloc] init] autorelease]; 
           chapterData.name = [NSString stringWithFormat:@"chapter_%d", (i+1)]; 
           chapterData.range =  
             CMTimeRangeMake(CMTimeMakeWithSeconds(i * chapterDuration, 10000),  
             CMTimeMakeWithSeconds(chapterDuration, 10000)); 
   
           [chapters addObject:chapterData]; 
       } 
   
       vaTrackingMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above.
   ```
