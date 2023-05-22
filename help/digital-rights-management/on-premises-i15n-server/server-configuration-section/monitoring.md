---
title: 監視
description: 監視
copied-description: true
exl-id: edf62298-4082-4ac1-b2b7-8d0e0959ed04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 監視{#monitoring}

個性化伺服器和密鑰生成伺服器均具有狀態頁，您可以使用該頁來確定伺服器的運行狀況。

* **個性化狀態頁：** [!DNL https://SERVER:PORT/flashaccess/status]

   * 如果應用程式伺服器正在運行且應用程式可以向密鑰生成伺服器發出GET請求，則報告「活動」
   * 該頁報告「活動」或無。 未顯示有關應用程式的資訊，因此此頁可用於從防火牆外部進行監視。

* **「密鑰生成狀態」頁：** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * 如果應用伺服器正在運行，則報告「活動」
   * 所有密鑰生成URL必須只能在內部訪問

* **「個性化統計資訊」頁：** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * 包括有關個性化伺服器的統計資訊，如所服務的請求數和快取中可用的密鑰數
   * 此頁面只能在內部訪問

* **「密鑰生成統計資訊」頁：** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * 包括有關密鑰生成伺服器的統計資訊，如所服務的請求數和磁碟上可用的密鑰檔案數
   * 所有密鑰生成URL必須只能在內部訪問
