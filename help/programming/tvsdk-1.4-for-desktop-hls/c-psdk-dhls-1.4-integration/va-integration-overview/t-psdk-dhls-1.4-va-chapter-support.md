---
description: 'null'
seo-description: 'null'
seo-title: 實作章節支援
title: 實作章節支援
uuid: 85d14b83-7910-4f5d-9ef2-511de916abd6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 實作章節支援{#implement-chapter-support}

您可透過下列方式，在以TVSDK為基礎的應用程式中定義及追蹤視訊追蹤章節：

* 預設章節，由TVSDK內部管理。

   章節定義為每個廣告插播之間的時間。 例如，前段廣告插播和第一段中間廣告之間的時間定義為第一章。
* 自訂章節，這些章節由應用程式管理，並以CMS資料或應用程式用來定義章節的其他方式為基礎。

   定義及追蹤預設或自訂章節。

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaMetadata.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example: 3 chapters of 60 second duration each 
   
       var chapters:Vector.<VideoAnalyticsChapterData> = new Vector.<VideoAnalyticsChapterData>(); 
       var chapterDuration:int = 60; 
       for (var i:int = 0; i < 3; i++) { 
           var chapterData:VideoAnalyticsChapterData =  
             new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration); 
           chapterData.name = "chapter_%d" + (i+1); 
   
           chapters.push(chapterData); 
       } 
   
       vaMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above. 
   ```

