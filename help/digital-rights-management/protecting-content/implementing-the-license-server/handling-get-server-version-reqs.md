---
title: 處理取得伺服器版本要求
description: 處理取得伺服器版本要求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 處理Get Server Version Requests {#handle-get-server-version-requests}

Adobe PrimetimeDRM客戶端3.0或更高版本發送「獲取伺服器版本」請求，以確定伺服器的功能。 所有使用Primetime DRM SDK 3.0或更新版本的伺服器都必須實作取得伺服器版本要求的支援。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 請求URL必須是「中繼資料中的授權伺服器URL」+「 [!DNL /flashaccess/getServerVersion/v3]」

對於Primetime DRM SDK 4.0或更新版本，對「取得伺服器版本」要求的回應會向用戶端指出伺服器支援Primetime DRM通訊協定的3和4版。
