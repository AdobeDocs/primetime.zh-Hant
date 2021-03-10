---
description: 要使用Flash Player，請確保您的環境符合必要的要求。
title: Flash Player需求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---


# Flash Player要求{#flash-player-requirements}

要使用Flash Player，請確保您的環境符合必要的要求。

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

以下是Flash Player的要求：

* 若要播放`Primetime.js`，請至少安裝Flash Player23版。
* 要提示更新Flash Player23版或更新版本，請至少安裝Flash Player11.0.0版。

## 包裝要求{#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

使用Flash Player播放需要下列SWF檔案：

* 處理瀏覽器TVSDK API的主要應用程式SWF檔案。
* 處理Flash Player安裝和更新的`playerProductInstall.swf` SWF檔案。

此外，Flash中的視訊播放需要授權Token檔案，該檔案可能是SWF或`.DAT`檔案。 SWF檔案的路徑、授權Token檔案，以及Token檔案名稱和類型，都可使用AdobePSDK API來指定。

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

