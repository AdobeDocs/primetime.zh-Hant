---
title: 監控
description: 監控
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 監控{#monitoring}

個人化伺服器和密鑰生成伺服器各有一個狀態頁，您可使用該狀態頁確定伺服器的運行狀況。

* **個人化狀態頁面：** [!DNL https://SERVER:PORT/flashaccess/status]

   * 如果應用程式伺服器正在執行且應用程式可向Key Generation伺服器提出GET要求，則報告「Alive」（活動）
   * 頁面會報告「活動」或無內容。 不會透露應用程式的資訊，因此本頁面可用於防火牆外部的監控。

* **「密鑰生成狀態」頁：** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * 如果應用程式伺服器正在執行，則報告「活動」
   * 所有金鑰產生URL必須僅能在內部存取

* **「個性化統計資訊」頁：** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * 包含個人化伺服器的統計資料，例如已處理的請求數和快取中可用的金鑰數
   * 此頁面僅能在內部存取

* **「密鑰生成統計資訊」頁：** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * 包含關於密鑰生成伺服器的統計資訊，如所服務的請求數和磁碟上可用的密鑰檔案數
   * 所有金鑰產生URL必須僅能在內部存取

