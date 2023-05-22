---
title: 實施章節支援
description: 實施章節支援
copied-description: true
exl-id: 8a962706-50cd-41c2-96a7-6af1b24145a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# 實施章節支援{#implement-chapter-support}

本章定義為每個廣告中斷之間的時間。 例如，預卷和中卷之間的時間定義為第一章。 您可以使用自定義章節在基於瀏覽器TVSDK的應用程式中定義和跟蹤視頻跟蹤的章節。 自定義章節由應用程式管理，並基於CMS資料或應用程式用於定義章節的其他方式。

1. 定義和跟蹤自定義章節。

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
