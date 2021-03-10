---
description: 如果應用程式需要處理從功能管理員傳送的事件，則需要在PlayerFragment.java檔案中註冊管理員。
title: 處理事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 4%

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
