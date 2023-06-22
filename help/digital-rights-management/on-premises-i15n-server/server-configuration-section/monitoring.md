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

「個人化」伺服器和「金鑰產生」伺服器各自都有狀態頁面，您可以使用此頁面來判斷伺服器的健康狀態。

* **個人化狀態頁面：** [!DNL https://SERVER:PORT/flashaccess/status]

   * 如果應用程式伺服器執行中，且應用程式可向金鑰產生伺服器發出GET要求，則會回報「使用中」
   * 頁面會報告「使用中」或沒有任何內容。 應用程式的相關資訊未顯示，因此此頁面可用於從防火牆外部進行監視。

* **金鑰產生狀態頁面：** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * 如果應用程式伺服器執行中，則報告「使用中」
   * 所有金鑰產生URL都只能由內部存取

* **「個人化統計資料」頁面：** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * 包含有關個人化伺服器的統計資料，例如提供的請求數和快取中可用的金鑰數
   * 此頁面只能供內部存取

* **金鑰產生統計值頁面：** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * 包括有關「金鑰產生」伺服器的統計資料，例如已服務的請求數和磁碟上可用的金鑰檔案數
   * 所有金鑰產生URL都只能由內部存取
