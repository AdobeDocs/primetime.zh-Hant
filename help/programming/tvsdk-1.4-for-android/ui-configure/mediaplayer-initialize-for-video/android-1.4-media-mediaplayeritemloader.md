---
description: 解析媒體資源的另一種方法是使用MediaPlayerItemLoader。 當您希望獲取有關特定媒體流的資訊而不實例化MediaPlayer實例時，此功能非常有用。
title: 使用MediaPlayerItemLoader載入媒體資源
exl-id: 9d129497-8a71-433a-a542-f49be519893b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader載入媒體資源 {#load-a-media-resource-using-mediaplayeritemloader}

解析媒體資源的另一種方法是使用MediaPlayerItemLoader。 當您希望獲取有關特定媒體流的資訊而不實例化MediaPlayer實例時，此功能非常有用。

通過 `MediaPlayerItemLoader` 類，可以為相應的 `MediaPlayerItem` 不將視圖附加到 `MediaPlayer` 實例，這將導致視頻解碼硬體資源的分配。 獲取 `MediaPlayerItem` 實例是非同步的。

1. 實施 `MediaPlayerItemLoader.LoaderListener` 回調介面。

       此介面定義兩種方法：
   
   * `LoaderListener.onError` 回調函式

      TVSDK使用此功能通知您的應用程式發生錯誤。 TVSDK提供錯誤代碼作為參數和包含診斷資訊的描述字串。

   * `LoaderListener.onError` 回調函式

      TVSDK使用此功能通知您的應用程式請求的資訊以 `MediaPlayerItem` 作為參數傳遞給回調的實例。

1. 將此實例作為參數傳遞給TVSDK的建構子，將其註冊到TVSDK `MediaPlayerItemLoader`。
1. 呼叫 `MediaPlayerItemLoader.load`，傳遞 `MediaResource` 的雙曲餘切值。

   的URL `MediaResource` 對象必須指向要獲取資訊的流。 例如：

   ```java
   // instantiate the listener interface 
   MediaPlayerItemLoader.LoaderListener _itemLoaderListener = 
     new MediaPlayerItemLoader.LoaderListener() { 
       @Override 
       public void onError(MediaErrorCode mediaErrorCode, String description) { 
           // something went wrong - look at the error code and description 
       } 
       @Override 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
           // information is available - look at the data in the "playerItem" object 
       } 
   } 
   
   // instantiate the MediaPlayerItemLoader object (pass the listener as parameter) 
   MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(_itemLoaderListener); 
   
   // create the MediaResource instance and set the URL to point to the actual media stream 
   MediaResource mediaResource =  
     MediaResource.createFromUrl("https://test.com/test_media.m3u8", null); 
   
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```
