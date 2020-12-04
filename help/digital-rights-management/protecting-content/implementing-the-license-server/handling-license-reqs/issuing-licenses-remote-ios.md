---
seo-title: 核發授權，以遠端傳送金鑰給iOS用戶端（需使用Adobe Primetime）
title: 核發授權，以遠端傳送金鑰給iOS用戶端（需使用Adobe Primetime）
uuid: 739dd93d-0645-4cb1-a3e8-aa78f7ef015e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 核發遠端密鑰傳送至iOS用戶端的授權（需使用Adobe Primetime）{#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

如果您想要針對需要針對iOS裝置傳送遠端金鑰的內容發行授權，您必須在`HandlerConfiguration.setKeyServerCertificate()`中指定金鑰伺服器的授權伺服器憑證。
