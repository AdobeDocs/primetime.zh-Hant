---
title: 疑難排解
description: 疑難排解
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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
