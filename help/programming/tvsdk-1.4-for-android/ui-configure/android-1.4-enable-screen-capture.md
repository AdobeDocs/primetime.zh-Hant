---
keywords: setSecure；VideoEngineView
title: 啟用熒幕擷取
description: 啟用熒幕擷取
copied-description: true
exl-id: 5dd1bf4e-ab50-4b57-89e4-eacc291a9fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# 啟用熒幕擷取{#enable-screen-capture}

TVSDK預設不允許熒幕擷取。 播放器呼叫 `setSecure(true)` 於 `com.adobe.ave.VideoEngineView` 建構時的物件。 由於您必須建構 `VideoEngineView` 物件並提供給 `VideoEngine` 物件。

若要在您的應用程式中啟用熒幕擷取：

1. 建構 `com.adobe.ave.VideoEngineView` 物件。
1. 呼叫 `setSecure(false)` 在您的 `VideoEngineView` 物件。
