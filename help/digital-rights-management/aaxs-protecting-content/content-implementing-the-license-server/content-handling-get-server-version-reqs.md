---
title: 處理獲取伺服器版本請求
description: 處理獲取伺服器版本請求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 處理獲取伺服器版本請求{#handling-get-server-version-requests}

Adobe存取用戶端3.0及更新版本會傳送「取得伺服器版本」要求，以判斷伺服器的功能。 所有使用Adobe存取SDK 3.0及更新版本的伺服器都必須實作取得伺服器版本要求的支援。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 請求URL必須是「中繼資料中的授權伺服器URL」+「/flashaccess/getServerVersion/v3」

對於Adobe存取SDK 4.0及更新版本，對「取得伺服器版本」要求的回應會向用戶端指出伺服器支援Adobe存取通訊協定的3和4版。
