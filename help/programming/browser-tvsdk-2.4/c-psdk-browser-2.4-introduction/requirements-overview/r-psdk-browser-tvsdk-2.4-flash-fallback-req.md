---
description: 要使用Flash Player，請確保您的環境滿足必要的要求。
title: Flash Player要求
exl-id: 26531d0d-d34c-4134-8a05-0604f00a3107
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Flash Player要求{#flash-player-requirements}

要使用Flash Player，請確保您的環境滿足必要的要求。

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

以下是Flash Player要求：

* 回放 `Primetime.js`，至少安裝Flash Player版本23。
* 要提示更新Flash Player版本23或更高版本，請至少安裝Flash Player版本11.0.0。

## 包裝要求 {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

使用Flash Player播放需要以下SWF檔案：

* 處理瀏覽器TVSDK API的主應用程式SWF檔案。
* 的 `playerProductInstall.swf` SWF檔案，處理Flash Player安裝和更新。

此外，Flash中的視頻播放需要授權令牌檔案，該檔案可能是SWF或 `.DAT` 的子菜單。 SWF檔案、授權令牌檔案以及令牌檔案名和類型的路徑可以使用AdobePSDK API指定。

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
