---
title: 處理Get Server版本要求
description: 處理Get Server版本要求
copied-description: true
exl-id: 125b0111-17e9-4f6f-954b-6975048cd2fa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 處理Get Server版本要求{#handling-get-server-version-requests}

Adobe Access client 3.0和更新版本會傳送Get Server Version要求，以判斷伺服器的功能。 所有使用Adobe存取SDK 3.0及更新版本的伺服器都必須實作支援，才能取得伺服器版本要求。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 請求URL必須是「中繼資料中的授權伺服器URL」+「/flashaccess/getServerVersion/v3」

若是Adobe存取SDK 4.0和更新版本，Get Server Version要求的回應會向使用者端指出伺服器支援Adobe存取通訊協定版本3和4。
