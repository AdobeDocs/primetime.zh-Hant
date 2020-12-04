---
description: 如果應用程式需要處理從功能管理員傳送的事件，則需要在PlayerFragment.java檔案中註冊管理員。
seo-description: 如果應用程式需要處理從功能管理員傳送的事件，則需要在PlayerFragment.java檔案中註冊管理員。
seo-title: 處理事件
title: 處理事件
uuid: 13639f02-0dcc-4a0a-8524-515da5478006
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 2%

---


# 處理事件{#handling-events}

如果應用程式需要處理從功能管理員傳送的事件，則需要在PlayerFragment.java檔案中註冊管理員。

例如：

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
