---
title: 處理Get Server版本要求
description: 處理Get Server版本要求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 處理Get Server版本要求{#handling-get-server-version-requests}

Adobe Access使用者端3.0和更新版本會傳送Get Server Version要求，以判斷伺服器的功能。 所有使用Adobe存取SDK 3.0及更高版本的伺服器都必須實作對「取得伺服器版本」要求的支援。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 請求URL必須是「中繼資料中的授權伺服器URL」+「/flashaccess/getServerVersion/v3」

對於Adobe Access SDK 4.0和更新版本，對「取得伺服器版本」要求的回應會向使用者端指出伺服器支援Adobe存取通訊協定版本3和版本4。
