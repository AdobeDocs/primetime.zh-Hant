---
title: 實作章節支援
description: 實作章節支援
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---


# 實作章節支援{#implement-chapter-support}

章節定義為每個廣告插播之間的時間。 例如，前段廣告插播和第一段中間廣告之間的時間定義為第一章。 您可以使用自訂章節，在以瀏覽器TVSDK為基礎的應用程式中定義及追蹤視訊追蹤章節。 自訂章節由應用程式管理，並以CMS資料或應用程式用來定義章節的其他方式為基礎。

1. 定義及追蹤自訂章節。

   ```js
   vaObj.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata: 
   // For example: 3 chapters of 60 second duration each 
   var chapters = []; 
   var chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       var chapterData = new AdobePSDK.VA.VideoAnalyticsChapterData("chapter_" + (i+1), i * chapterDuration, chapterDuration, (i+1)); 
       chapters.push(chapterData); 
   } 
   
   vaObj.chapters = chapters;
   ```

