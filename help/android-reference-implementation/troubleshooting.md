---
title: 疑難排除
description: 疑難排除
copied-description: true
exl-id: 618b1e19-d25d-435d-b118-b43455bde974
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# 疑難排除{#troubleshooting}

* 對於某些執行API層級10或更舊層級的舊裝置，由於許可權問題，logcat無法開啟記錄裝置。 會出現下列例外： `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **因應措施：**

   1. 開啟 [!DNL AndroidManifest.xml] 在 [!DNL CatalogActivity] 專案。

   1. 將下列許可權新增至 [!DNL `AndroidManfest.xml`] 檔案：

      ```
      android.permission.READ_LOGS
      ```
