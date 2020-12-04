---
seo-title: 疑難排解
title: 疑難排解
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# 疑難排解{#troubleshooting}

* 對於某些執行API等級10或更舊版本的舊版裝置，記錄檔無法開啟記錄檔裝置，因為權限問題。 出現以下例外：`java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **因應措施：**

   1. 在工作區的[!DNL CatalogActivity]專案下開啟[!DNL AndroidManifest.xml]。

   1. 將下列權限添加到[!DNL `AndroidManfest.xml`]檔案：

      ```
      android.permission.READ_LOGS
      ```
