---
description: 您可以使用回撥函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
title: 實作自訂中繼資料支援
exl-id: d2291649-79e2-4935-8980-4f2038d58342
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 實作自訂中繼資料支援{#implement-custom-metadata-support}

您可以使用回撥函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。

回呼函式會在進行追蹤呼叫之前叫用，因此您的應用程式可以附加廣告或章節專屬的中繼資料。

1. 為內容、廣告和章節叫用回呼函式。

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
