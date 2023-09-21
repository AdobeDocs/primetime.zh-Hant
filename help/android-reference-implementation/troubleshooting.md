---
title: 疑難排除
description: 疑難排除
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# 疑難排除{#troubleshooting}

* 對於某些執行API Level 10或更舊版本的舊裝置，由於許可權問題，logcat無法開啟記錄裝置。 會出現下列例外： `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **因應措施：**

   1. 開啟 [!DNL AndroidManifest.xml] 在 [!DNL CatalogActivity] 工作區中的專案。

   1. 將下列許可權新增至 [!DNL `AndroidManfest.xml`] 檔案：

      ```
      android.permission.READ_LOGS
      ```
