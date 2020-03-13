---
description: 您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
seo-description: 您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。
seo-title: 實作自訂中繼資料支援
title: 實作自訂中繼資料支援
uuid: 068ef0b9-79a2-4e44-8a0a-01e9deb8e4a6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 實作自訂中繼資料支援 {#implement-custom-metadata-support}

您可以使用回呼函式，針對內容、廣告和章節追蹤呼叫提供自訂中繼資料。

回呼函式會在進行追蹤呼叫之前呼叫，因此您的應用程式可以附加廣告或章節專屬的中繼資料。

叫用內容、廣告和章節的回呼函式。

```java
// Video Metadata Block 
vaMetadata.setVideoMetadataBlock(new VideoAnalyticsMetadata.VideoMetadataBlock() { 
    @Override 
    public HashMap<String, String> call() { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("myvideoid", "1234"); 
        result.put("mysdkversion", Version.getVersion()); 
  
        return result; 
    } 
}); 
  
// Ad Metadata Block invoked on every ad start 
vaMetadata.setAdMetadataBlock(new VideoAnalyticsMetadata.AdMetadataBlock() { 
    @Override 
    public HashMap<String, String> call(Ad ad) { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("myadid", "ad-1234"); 
        result.put("myad-sdkversion", Version.getVersion()); 
  
        return result; 
    } 
}); 
  
// Chapter Metadata Block invoked on every chapter start 
vaMetadata.setChapterMetadataBlock(new VideoAnalyticsMetadata.ChapterMetadataBlock() { 
    @Override 
    public HashMap<String, String> call(VideoAnalyticsChapterData chapter) { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("mychapterid", "chapter-1234"); 
        result.put("mychapter-sdkversion", Version.getVersion()); 
  
        return result; 
    } 
});
```

