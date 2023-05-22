---
title: 故障排除
description: 故障排除
copied-description: true
exl-id: 618b1e19-d25d-435d-b118-b43455bde974
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# 故障排除{#troubleshooting}

* 對於運行API級別10或更舊版本的某些較舊設備，由於權限問題，日誌無法開啟日誌設備。 出現以下異常： `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **解決方法：**

   1. 開啟 [!DNL AndroidManifest.xml] 下 [!DNL CatalogActivity] 的子菜單。

   1. 將以下權限添加到 [!DNL `AndroidManfest.xml`] 檔案：

      ```
      android.permission.READ_LOGS
      ```
