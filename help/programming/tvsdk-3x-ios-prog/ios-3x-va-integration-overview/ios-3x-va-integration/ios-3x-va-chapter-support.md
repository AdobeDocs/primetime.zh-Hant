---
title: 實作章節支援
description: 實作章節支援
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 實作章節支援 {#implement-chapter-support}

您可以透過下列方式，在TVSDK型應用程式中定義及追蹤視訊追蹤的章節：

* 預設章節，由TVSDK內部管理。

  章節定義為每個廣告插播之間的時間。 例如，前段廣告插播和第一個中段之間的時間會定義為第一個章節。
* 自訂章節，由應用程式管理，並以CMS資料或應用程式用來定義章節的其他方式為基礎。

  定義及追蹤預設或自訂章節。

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
