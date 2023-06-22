---
title: 核發遠端金鑰傳遞至iOS使用者端的授權(需要Adobe Primetime)
description: 核發遠端金鑰傳遞至iOS使用者端的授權(需要Adobe Primetime)
copied-description: true
exl-id: f9f13ab3-3394-4729-a64c-f28c67601e26
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 核發遠端金鑰傳遞至iOS使用者端的授權(需要Adobe Primetime){#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

如果您想要針對iOS裝置需要遠端金鑰傳遞的內容核發授權，您需要指定金鑰伺服器的授權伺服器憑證 `HandlerConfiguration.setKeyServerCertificate()`.
