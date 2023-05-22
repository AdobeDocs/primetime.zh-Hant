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

為了確保對個性化伺服器的訪問安全，只需暴露某些應用程式路徑。 個性化伺服器必須接受客戶端到以下路徑的請求：

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

服務路徑，如 [!DNL /flashaccess/admin/*] （即，狀態和管理頁）只能從防火牆內訪問。 不應從防火牆外部訪問密鑰生成伺服器的任何部分。
