---
description: 若要使用Flash Player，請確保您的環境符合必要的需求。
title: Flash Player需求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Flash Player需求{#flash-player-requirements}

若要使用Flash Player，請確保您的環境符合必要的需求。

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

以下是Flash Player的需求：

* 播放 `Primetime.js`，至少安裝Flash Player版本23。
* 若要提示更新Flash Player版本23或更新版本，請至少安裝Flash Player版本11.0.0。

## 封裝需求 {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

使用Flash Player播放需要下列SWF檔案：

* 處理瀏覽器TVSDK API的主要應用程式SWF檔案。
* 此 `playerProductInstall.swf` 處理Flash Player安裝和更新的SWF檔案。

此外，Flash中的視訊播放需要授權權杖檔案，該檔案可能是SWF或 `.DAT` 檔案。 SWF檔案的路徑、授權權杖檔案以及權杖檔案名稱和型別可以使用AdobePSDK API來指定。

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
