---
description: 解析媒體資源的另一種方法是使用MediaPlayerItemLoader。 如果您想要取得特定媒體資料流的相關資訊，但不具現化MediaPlayer執行個體，這會很有用。
title: 使用MediaPlayerItemLoader載入媒體資源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader載入媒體資源 {#load-a-media-resource-using-mediaplayeritemloader}

解析媒體資源的另一種方法是使用MediaPlayerItemLoader。 如果您想要取得特定媒體資料流的相關資訊，但不具現化MediaPlayer執行個體，這會很有用。

透過 `MediaPlayerItemLoader` 類別中，您可以交換媒體資源以取得對應的 `MediaPlayerItem` 而不將檢視附加至 `MediaPlayer` 執行個體，這會配置視訊解碼硬體資源。 取得「 」的程式 `MediaPlayerItem` 執行個體為非同步。

1. 實作 `MediaPlayerItemLoader.LoaderListener` 回呼介面。

       此介面會定義兩種方法：
   
   * `LoaderListener.onError` 回呼函式

     TVSDK會使用此功能，通知您的應用程式已發生錯誤。 TVSDK提供錯誤碼作為引數，以及包含診斷資訊的說明字串。

   * `LoaderListener.onError` 回呼函式

     TVSDK會使用此資訊來通知您的應用程式，要求資訊可以以下列形式提供： `MediaPlayerItem` 作為引數傳遞給callback的例項。

1. 將此執行個體當作引數傳遞至的建構函式，以註冊至TVSDK。 `MediaPlayerItemLoader`.
1. 呼叫 `MediaPlayerItemLoader.load`，傳遞的例項 `MediaResource` 物件。

   的URL `MediaResource` 物件必須指向您要取得資訊的資料流。 例如：

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
