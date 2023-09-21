---
keywords: setSecure；VideoEngineView
title: 啟用熒幕擷取
description: 啟用熒幕擷取
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# 啟用熒幕擷取{#enable-screen-capture}

TVSDK預設不允許熒幕擷取。 播放器呼叫 `setSecure(true)` 於 `com.adobe.ave.VideoEngineView` 建構時的物件。 您必須建構物件才能存取此物件 `VideoEngineView` 物件並提供給 `VideoEngine` 物件。

若要啟用應用程式中的熒幕擷取：

1. 建構 `com.adobe.ave.VideoEngineView` 物件。
1. 呼叫 `setSecure(false)` 在您的 `VideoEngineView` 物件。
