---
seo-title: 處理取得伺服器版本要求
title: 處理取得伺服器版本要求
uuid: 6e287f58-2ad2-428a-a76a-6847d06b0fd8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 處理取得伺服器版本要求 {#handle-get-server-version-requests}

Adobe Primetime DRM用戶端3.0或更新版本會傳送「取得伺服器版本」要求，以決定伺服器的功能。 所有使用Primetime DRM SDK 3.0或更新版本的伺服器都必須實作取得伺服器版本要求的支援。

* 請求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 請求URL必須是「中繼資料中的授權伺服器URL」+「 [!DNL /flashaccess/getServerVersion/v3]」

對於Primetime DRM SDK 4.0或更新版本，對「取得伺服器版本」要求的回應會向用戶端指出伺服器支援Primetime DRM通訊協定的3和4版。
