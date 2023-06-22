---
title: 防火牆規則
description: 防火牆規則
copied-description: true
exl-id: 1a40822a-893d-43ec-9c3e-8e0b4ebe6d01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 防火牆規則{#firewall-rules}

若要安全地存取個人化伺服器，只需要公開某些應用程式路徑。 個人化伺服器必須接受使用者端對下列路徑的請求：

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

服務路徑，例如 [!DNL /flashaccess/admin/*] （即狀態和管理頁面）只能從防火牆記憶體取。 不應從防火牆外部存取金鑰產生伺服器的任何部分。
