---
description: 解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。
seo-description: 解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。
seo-title: 使用MediaPlayerItemLoader載入媒體資源
title: 使用MediaPlayerItemLoader載入媒體資源
uuid: b2311ddc-f059-4775-8553-fc354ec2636b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# 使用MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}載入媒體資源

解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。

通過`MediaPlayerItemLoader`類，您可以為相應的`MediaPlayerItem`交換媒體資源，而不將視圖附加到`MediaPlayer`實例，這將導致視頻解碼硬體資源的分配。 獲取`MediaPlayerItem`實例的過程是非同步的。

1. 實作`MediaPlayerItemLoader.LoaderListener`回呼介面。

       此介面定義了兩種方法：
   
   * `LoaderListener.onError` 回調函式

      TVSDK會使用此項來通知您的應用程式發生錯誤。 TVSDK提供錯誤碼作為參數，以及包含診斷資訊的描述字串。

   * `LoaderListener.onError` 回調函式

      TVSDK會使用此資訊通知您的應用程式，要求的資訊以`MediaPlayerItem`例項的形式提供，並作為回呼的參數傳遞。

1. 將此例項作為參數傳遞至`MediaPlayerItemLoader`的建構函式，以註冊至TVSDK。
1. 呼叫`MediaPlayerItemLoader.load`，傳遞`MediaResource`物件的例項。

   `MediaResource`物件的URL必須指向您要取得資訊的串流。 例如：

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

