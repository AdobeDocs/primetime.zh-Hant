---
description: 如果應用程式需要處理從功能管理員傳送的事件，則需要在PlayerFragment.java檔案中註冊管理員。
title: 處理事件
exl-id: 4c9a76bb-071e-4408-819c-a7611fe615cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
