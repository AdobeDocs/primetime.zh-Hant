---
description: 'null'
seo-description: 'null'
seo-title: 新增廣告
title: 新增廣告
uuid: 7762506f-b55e-445d-b8a2-c1208358a370
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---


# 新增廣告{#add-advertising}

1. 定義廣告中繼資料。

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. 將廣告中繼資料新增至`MediaResource`。

   ```js
   var mediaResource =  
     new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
   ```

1. 將設定添加到配置並添加`SpliceOut`解析器工廠。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings; 
   config.advertisingFactory = new ExtCueOutContentFactory(auditudeSettings);
   ```

1. 將`ExtCueOutContentFactory`新增至程式庫區段。
1. 從程式庫區段下載`ExtCueOutContentFactory.js`，並將它放置在工作資料夾中。

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. 測試您的設定。
