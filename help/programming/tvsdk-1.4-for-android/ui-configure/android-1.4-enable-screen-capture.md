---
keywords: setSecure;VideoEngineView
title: 啟用螢幕擷取
description: 啟用螢幕擷取
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# 啟用螢幕擷取{#enable-screen-capture}

依預設，TVSDK不允許螢幕擷取。 播放器在構建時對`com.adobe.ave.VideoEngineView`對象調用`setSecure(true)`。 您可以訪問此對象，因為必須構造`VideoEngineView`對象並將其提供給`VideoEngine`對象。

若要在您的應用程式中啟用螢幕擷取：

1. 構建`com.adobe.ave.VideoEngineView`對象。
1. 在`VideoEngineView`物件上呼叫`setSecure(false)`。
