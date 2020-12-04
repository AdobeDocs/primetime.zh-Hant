---
description: 您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
seo-description: 您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
seo-title: 實作自訂中繼資料支援
title: 實作自訂中繼資料支援
uuid: 2186db58-10b0-43a6-840f-53ab289843ee
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

   ```
   // Video Metadata Block 
   vaMetadata.videoMetadataBlock = function():Object { 
       return {"myvideoid":"1234", "mysdkversion":Version.version} 
   }; 
   
   // Ad Metadata Block invoked on every ad start 
   vaMetadata.adMetadataBlock = function(ad:Ad):Object { 
       return {"myadid":"ad-1234", "myad-sdkversion":Version.version} 
   }; 
   
   // Chapter Metadata Block invoked on every chapter start 
   vaMetadata.chapterMetadataBlock = function(chapter:VideoAnalyticsChapterData) { 
       return {"mychapterid":"chapter-1234", "mychapter-sdkversion":Version.version} 
   };
   ```

