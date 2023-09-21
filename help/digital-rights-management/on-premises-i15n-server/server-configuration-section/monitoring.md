---
title: 監視
description: 監視
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 監視{#monitoring}

「個人化」伺服器和「金鑰產生」伺服器各自都有狀態頁面，您可以使用它來判斷伺服器的健康狀態。

* **個人化狀態頁面：** [!DNL https://SERVER:PORT/flashaccess/status]

   * 如果應用程式伺服器執行中，且應用程式可向金鑰產生伺服器發出GET要求，則會回報「使用中」
   * 頁面報告「使用中」或沒有內容。 應用程式的相關資訊不會顯示，因此此頁面可用於從防火牆外部進行監視。

* **金鑰產生狀態頁面：** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * 如果應用程式伺服器執行中，會報告「使用中」
   * 所有金鑰產生URL都只能由內部存取

* **「個人化統計值」頁面：** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * 包含有關個人化伺服器的統計資料，例如提供的請求數和快取中可用的金鑰數
   * 此頁面只能供內部存取

* **金鑰產生統計資料頁面：** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * 包括有關「金鑰產生」伺服器的統計資料，例如提供的要求數目以及磁碟上可用的金鑰檔案數目
   * 所有金鑰產生URL都只能由內部存取
