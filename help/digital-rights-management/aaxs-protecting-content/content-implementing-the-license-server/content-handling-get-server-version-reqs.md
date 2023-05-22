---
title: 處理獲取伺服器版本請求
description: 處理獲取伺服器版本請求
copied-description: true
exl-id: 125b0111-17e9-4f6f-954b-6975048cd2fa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 處理獲取伺服器版本請求{#handling-get-server-version-requests}

AdobeAccess客戶端3.0及更高版本會發送獲取伺服器版本請求以確定伺服器的功能。 所有使用Adobe訪問SDK 3.0及更高版本的伺服器都必須支援獲取伺服器版本請求。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 請求URL必須是「元資料中的許可證伺服器URL」+「/flashaccess/getServerVersion/v3」

對於Adobe訪問SDK 4.0及更高版本，對「獲取伺服器版本」請求的響應會向客戶端指示伺服器支援Adobe訪問協定的3和4版。
