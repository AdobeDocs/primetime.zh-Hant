---
description: 解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。
seo-description: 解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。
seo-title: 使用MediaPlayerItemLoader載入媒體資源
title: 使用MediaPlayerItemLoader載入媒體資源
uuid: b2311ddc-f059-4775-8553-fc354ec2636b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 使用MediaPlayerItemLoader載入媒體資源 {#load-a-media-resource-using-mediaplayeritemloader}

解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。

通過類 `MediaPlayerItemLoader` 別，您可以交換對應的媒體資源，而不將視圖附加到 `MediaPlayerItem``MediaPlayer` 實例，這會導致視頻解碼硬體資源的分配。 獲取實例的過 `MediaPlayerItem` 程是非同步的。

1. 實作回 `MediaPlayerItemLoader.LoaderListener` 呼介面。

       此介面定義了兩種方法：
   
   * `LoaderListener.onError` 回調函式

      TVSDK會使用此項來通知您的應用程式發生錯誤。 TVSDK提供錯誤碼作為參數，以及包含診斷資訊的描述字串。

   * `LoaderListener.onError` 回調函式

      TVSDK會使用此項來通知您的應用程式，請求的資訊以例項的形式提供，而 `MediaPlayerItem` 該例項會作為回呼的參數傳遞。

1. 將此例項作為參數傳入至TVSDK的建構函式，以註冊此例項 `MediaPlayerItemLoader`。
1. 呼 `MediaPlayerItemLoader.load`叫，傳遞物件的例 `MediaResource` 項。

   物件的URL `MediaResource` 必須指向您要取得資訊的串流。 例如：

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

