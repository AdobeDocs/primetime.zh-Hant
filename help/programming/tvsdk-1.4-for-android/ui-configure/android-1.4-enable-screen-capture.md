---
keywords: setSecure;VideoEngineView
title: 啟用螢幕捕獲
description: 啟用螢幕捕獲
copied-description: true
exl-id: 5dd1bf4e-ab50-4b57-89e4-eacc291a9fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# 啟用螢幕捕獲{#enable-screen-capture}

預設情況下，TVSDK不允許螢幕捕獲。 玩家呼叫 `setSecure(true)` 的 `com.adobe.ave.VideoEngineView` 在構造時對象。 您有權訪問此對象，因為您必須構造 `VideoEngineView` 並提供給 `VideoEngine` 的雙曲餘切值。

要在應用中啟用螢幕捕獲：

1. 構建 `com.adobe.ave.VideoEngineView` 的雙曲餘切值。
1. 呼叫 `setSecure(false)` 在 `VideoEngineView` 的雙曲餘切值。
