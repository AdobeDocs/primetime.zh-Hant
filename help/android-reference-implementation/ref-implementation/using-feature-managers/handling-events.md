---
description: 如果應用程式需要處理從功能管理員傳送的事件，則需要在PlayerFragment.java檔案中註冊管理員。
title: 處理事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# 處理事件 {#handling-events}

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
