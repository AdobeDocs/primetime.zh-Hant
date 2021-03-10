---
title: 實作章節支援
description: 實作章節支援
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# 實作章節支援{#implement-chapter-support}

您可以在TVSDK應用程式中定義並追蹤&#x200B;*custom*&#x200B;章節，以進行視訊追蹤。

自訂章節由應用程式管理，並以CMS資料或應用程式用來定義章節的其他方式為基礎。

>[!CAUTION]
>
>3.0 Android TVSDK不支援預設章節。

定義及追蹤自訂章節。

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
