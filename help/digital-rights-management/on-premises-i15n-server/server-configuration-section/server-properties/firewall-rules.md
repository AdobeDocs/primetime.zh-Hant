---
title: 防火牆規則
description: 防火牆規則
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 防火牆規則{#firewall-rules}

為確保對個人化伺服器的訪問安全，只需公開某些應用程式路徑。 個人化伺服器必須接受客戶端到以下路徑的請求：

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

服務路徑(如[!DNL /flashaccess/admin/*]（即狀態和管理頁）)只能從防火牆內訪問。 不應從防火牆外部訪問密鑰生成伺服器的任何部分。
