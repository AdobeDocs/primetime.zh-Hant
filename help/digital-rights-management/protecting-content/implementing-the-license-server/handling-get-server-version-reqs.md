---
title: 處理獲取伺服器版本請求
description: 處理獲取伺服器版本請求
copied-description: true
exl-id: 86a1bbe3-2ae4-4d4e-be51-fbbeb32147c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 處理獲取伺服器版本請求 {#handle-get-server-version-requests}

Adobe PrimetimeDRM客戶端3.0或更高版本發送「獲取伺服器版本」請求以確定伺服器的功能。 所有使用Mogfire DRM SDK 3.0或更高版本的伺服器必須實現對獲取伺服器版本請求的支援。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 請求URL必須是&quot;元資料中的許可證伺服器URL&quot;+ &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

對於黃金時段DRM SDK 4.0或更高版本，對獲取伺服器版本請求的響應向客戶端指示伺服器支援黃金時段DRM協定的版本3和4。
