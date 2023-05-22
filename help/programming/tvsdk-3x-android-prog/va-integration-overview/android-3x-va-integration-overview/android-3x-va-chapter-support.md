---
title: 實施章節支援
description: 實施章節支援
copied-description: true
exl-id: 2db335b3-1d9b-4339-b1b6-e12ee0f06566
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# 實施章節支援 {#implement-chapter-support}

您可以定義和跟蹤 *自定義* 用於基於TVSDK的應用程式中視頻跟蹤的章節。

自定義章節由應用程式管理，並基於CMS資料或應用程式用於定義章節的另一種方式。

>[!CAUTION]
>
>3.0 Android TVSDK不支援預設章節。

定義和跟蹤自定義章節。

```java
// First, enable chapter tracking by setting   
// enableChapterTracking to true: 
 
vaMetadata.enableChapterTracking(true); 
// For custom chapter definitions, provide  
// an array list of chapters through the metadata. 
// For example: 3 chapters of 60 second duration each 
 
List<VideoAnalyticsChapterData> chapters =  
  new ArrayList<VideoAnalyticsChapterData>(); 
 
Int chapterDuration = 60; 
for (var i = 0; i < 3; i++) { 
    VideoAnalyticsChapterData chapterData =  
      new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
    chapterData.setName("chapter_" + (i+1)); 
    chapters.add(chapterData); 
} 
 
vaMetadata.setChapters(chapters); 
```
