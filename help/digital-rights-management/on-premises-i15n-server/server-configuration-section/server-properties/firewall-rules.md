---
title: 防火牆規則
description: 防火牆規則
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 防火牆規則{#firewall-rules}

若要保護對個人化伺服器的存取安全，只需要公開某些應用程式路徑。 Individualization伺服器必須接受使用者端對以下路徑的請求：

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

服務路徑，例如 [!DNL /flashaccess/admin/*] （即狀態和管理頁面）只能從防火牆記憶體取。 不應從防火牆外部存取金鑰產生伺服器的任何部分。
