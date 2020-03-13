---
description: 若要使用Flash Player，請確保您的環境符合必要的需求。
seo-description: 若要使用Flash Player，請確保您的環境符合必要的需求。
seo-title: Flash Player需求
title: Flash Player需求
uuid: f181457b-2bb4-4baa-b2b7-d787f65fab75
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Flash Player需求{#flash-player-requirements}

若要使用Flash Player，請確保您的環境符合必要的需求。

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

以下是Flash Player的需求：

* 若要播放， `Primetime.js`請至少安裝Flash Player 23版。
* 若要提示更新Flash Player 23或更新版本，請至少安裝Flash Player 11.0.0版。

## 封裝需求 {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

使用Flash Player播放時需要下列SWF檔案：

* 處理瀏覽器TVSDK API的主要應用程式SWF檔案。
* 處理 `playerProductInstall.swf` Flash Player安裝與更新的SWF檔案。

此外，在Flash中播放視訊時，需要授權Token檔案，可能是SWF或 `.DAT` 檔案。 SWF檔案的路徑、授權Token檔案，以及Token檔案名稱和類型，都可使用AdobePSDK API來指定。

例如：

```js
// Set relative or http path to directory containing SWF.  
// Defaults to current directory for the html page. 
AdobePSDK.setSWFPath(<swfPath>); 
 
// Set the relative or http path to directory containing token file(s). 
// Defaults to SWFPath + "token/". 
AdobePSDK.setAuthorizationTokenPath(<authorizationTokenPath>); 
 
// Set the name of the token file, do not include any path in this string. 
AdobePSDK.setAuthorizationTokenFilename("hlsaf_localhost.swf"); 
 
//Set the token type, "DAT" or "SWF". Defaults to "DAT" 
AdobePSDK.setAuthorizationTokenType("SWF");
```

