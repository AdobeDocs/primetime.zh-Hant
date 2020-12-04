---
description: 您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
seo-description: 您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
seo-title: 實作自訂中繼資料支援
title: 實作自訂中繼資料支援
uuid: 6e23311c-a393-4485-919e-4cf6412789b1
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# 實作自訂中繼資料支援{#implement-custom-metadata-support}

您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。

回呼函式會在進行追蹤呼叫之前呼叫，因此您的應用程式可以附加廣告或章節專屬的中繼資料。

1. 叫用內容、廣告和章節的回呼函式。

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

