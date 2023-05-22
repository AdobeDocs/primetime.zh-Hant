---
title: 為iOS客戶端發放遠程密鑰傳遞許可證(需要Adobe Primetime)
description: 為iOS客戶端發放遠程密鑰傳遞許可證(需要Adobe Primetime)
copied-description: true
exl-id: 91eecc25-16a9-4f8c-9307-83e70bb77d68
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---

# 為iOS客戶端發放遠程密鑰傳遞許可證(需要Adobe Primetime){#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

為了為需要為iOS設備提供遠程密鑰傳遞的內容頒發許可證，必須在中指定密鑰伺服器的許可證伺服器證書 `HandlerConfiguration.setKeyServerCertificate()`。
