---
title: 實作章節支援
description: 實作章節支援
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# 實作章節支援{#implement-chapter-support}

章節定義為每個廣告插播之間的時間。 例如，前段廣告插播和第一個中段之間的時間會定義為第一個章節。 您可以使用自訂章節，在瀏覽器TVSDK型應用程式中定義及追蹤視訊追蹤的章節。 自訂章節是由應用程式管理，且以CMS資料或應用程式用來定義章節的其他方式為基礎。

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
