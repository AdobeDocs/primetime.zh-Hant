---
title: 為iOS用戶端發放遠端金鑰的授權(需要Adobe Primetime)
description: 為iOS用戶端發放遠端金鑰的授權(需要Adobe Primetime)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 為iOS客戶端發放遠程密鑰傳遞許可證(需要Adobe Primetime){#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

如果您想要針對需要針對iOS裝置傳送遠端金鑰的內容發行授權，您必須在`HandlerConfiguration.setKeyServerCertificate()`中指定金鑰伺服器的授權伺服器憑證。
