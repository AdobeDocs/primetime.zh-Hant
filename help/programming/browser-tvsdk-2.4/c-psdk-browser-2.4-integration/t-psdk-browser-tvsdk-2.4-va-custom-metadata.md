---
description: 您可以使用回調函式提供有關內容、廣告和章節跟蹤調用的自定義元資料。
title: 實施自定義元資料支援
exl-id: d2291649-79e2-4935-8980-4f2038d58342
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 實施自定義元資料支援{#implement-custom-metadata-support}

您可以使用回調函式提供有關內容、廣告和章節跟蹤調用的自定義元資料。

回調函式在進行跟蹤調用之前即被調用，因此您的應用程式可以附加特定於廣告或章節的元資料。

1. 調用內容、廣告和章節的回調函式。

   ```js
   vaObj.videoMetadataBlock = function() { 
       return { 
           "name" : "my-video", 
           "genre" : "comedy" 
       }; 
   } 
   
   vaObj.adMetadataBlock = function(ad) { 
       return { 
           "name" : "my-ad", 
           "category" : "automotive" 
       }; 
   } 
   
   vaObj.chapterMetadataBlock = function(chapter) { 
       return { 
           "name" : "my-chapter", 
           "type" : "quartile" 
       }; 
   }
   ```
