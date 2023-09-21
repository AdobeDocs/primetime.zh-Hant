---
title: 核發遠端金鑰傳遞至iOS使用者端的授權(需要Adobe Primetime)
description: 核發遠端金鑰傳遞至iOS使用者端的授權(需要Adobe Primetime)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 核發遠端金鑰傳遞至iOS使用者端的授權(需要Adobe Primetime){#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

如果您想要針對iOS裝置需要遠端金鑰傳遞的內容發行授權，則必須在中指定金鑰伺服器的授權伺服器憑證 `HandlerConfiguration.setKeyServerCertificate()`.
