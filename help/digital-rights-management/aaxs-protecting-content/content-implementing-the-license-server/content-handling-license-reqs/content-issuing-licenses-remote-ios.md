---
title: 核發遠端金鑰傳遞至iOS使用者端的授權(需要Adobe Primetime)
description: 核發遠端金鑰傳遞至iOS使用者端的授權(需要Adobe Primetime)
copied-description: true
exl-id: 91eecc25-16a9-4f8c-9307-83e70bb77d68
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---

# 核發遠端金鑰傳遞至iOS使用者端的授權(需要Adobe Primetime){#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

為了針對iOS裝置需要遠端金鑰傳遞的內容發行授權，金鑰伺服器的授權伺服器憑證必須在 `HandlerConfiguration.setKeyServerCertificate()`.
