---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: 啟用螢幕擷取
title: 啟用螢幕擷取
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 啟用螢幕擷取{#enable-screen-capture}

依預設，TVSDK不允許螢幕擷取。 玩家在建 `setSecure(true)` 構時 `com.adobe.ave.VideoEngineView` 呼叫物件。 您可以訪問此對象，因為必須構造對 `VideoEngineView` 像並提供給該對 `VideoEngine` 像。

若要在您的應用程式中啟用螢幕擷取：

1. 建構物 `com.adobe.ave.VideoEngineView` 件。
1. 呼叫 `setSecure(false)` 您的 `VideoEngineView` 物件。
