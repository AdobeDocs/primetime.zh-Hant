---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: 啟用螢幕擷取
title: 啟用螢幕擷取
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# 啟用螢幕擷取{#enable-screen-capture}

依預設，TVSDK不允許螢幕擷取。 播放器在構建時對`com.adobe.ave.VideoEngineView`對象調用`setSecure(true)`。 您可以訪問此對象，因為必須構造`VideoEngineView`對象並將其提供給`VideoEngine`對象。

若要在您的應用程式中啟用螢幕擷取：

1. 構建`com.adobe.ave.VideoEngineView`對象。
1. 在`VideoEngineView`物件上呼叫`setSecure(false)`。
