---
title: 處理取得伺服器版本要求
description: 處理取得伺服器版本要求
copied-description: true
exl-id: 86a1bbe3-2ae4-4d4e-be51-fbbeb32147c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 處理取得伺服器版本要求 {#handle-get-server-version-requests}

Adobe Primetime DRM使用者端3.0或更新版本會傳送取得伺服器版本要求，以判斷伺服器的功能。 所有使用Primetime DRM SDK 3.0或更新版本的伺服器都必須實作取得伺服器版本要求的支援。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 請求URL必須是「中繼資料中的授權伺服器URL」+ &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

對於Primetime DRM SDK 4.0或更新版本，對「取得伺服器版本」要求的回應會向使用者端指出伺服器支援Primetime DRM通訊協定版本3和4。
