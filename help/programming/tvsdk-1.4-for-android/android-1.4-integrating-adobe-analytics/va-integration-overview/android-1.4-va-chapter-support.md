---
title: 實作章節支援
description: 實作章節支援
copied-description: true
exl-id: f86af555-4eba-4bc8-a323-41f65f23f4cc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 實作章節支援 {#implement-chapter-support}

您可以透過下列方式，在以TVSDK為主的應用程式中定義及追蹤視訊追蹤的章節：

* 預設章節，由TVSDK內部管理。

   章節定義為每個廣告插播之間的時間。 例如，前段廣告插播和第一個中段之間的時間會定義為第一個章節。
* 自訂章節，由應用程式管理，並以CMS資料或應用程式用來定義章節的其他方式為基礎。

1. 定義及追蹤預設或自訂章節。

   ```java
   // First, enable chapter tracking by setting  
   // the Boolean 'enableChapterTracking' to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide an array list of chapters  
   // through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters = new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   // For default chapters, the application must not set  
   // custom chapters on the tracking metadata 
   // and simply enable chapters to be tracked by setting  
   // the boolean value as defined above.
   ```
