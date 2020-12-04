---
seo-title: 處理獲取伺服器版本請求
title: 處理獲取伺服器版本請求
uuid: a3084faa-cf3d-45cc-a244-298308c4cf15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 處理獲取伺服器版本請求{#handling-get-server-version-requests}

Adobe Access用戶端3.0及更新版本會傳送「取得伺服器版本」要求，以判斷伺服器的功能。 所有使用Adobe Access SDK 3.0及更新版本的伺服器都必須實作取得伺服器版本要求的支援。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 請求URL必須是「中繼資料中的授權伺服器URL」+「/flashaccess/getServerVersion/v3」

對於Adobe Access SDK 4.0及更新版本，回應「取得伺服器版本」要求時，會向用戶端指出伺服器支援Adobe Access通訊協定的3和4版。
