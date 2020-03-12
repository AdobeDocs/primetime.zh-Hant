---
seo-title: 疑難排解
title: 疑難排解
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 疑難排解{#troubleshooting}

* 對於某些執行API等級10或更舊版本的舊版裝置，記錄檔無法開啟記錄檔裝置，因為權限問題。 出現以下例外：解 `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` 決 **方法：**

   1. 在工 [!DNL AndroidManifest.xml] 作區 [!DNL CatalogActivity] 的專案下開啟。

   1. 將下列權限新增至檔 [!DNL `AndroidManfest.xml`] 案：

      ```
      android.permission.READ_LOGS
      ```
