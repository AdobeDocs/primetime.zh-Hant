---
title: 使用黃金時段DRM密鑰伺服器的要求
description: 使用黃金時段DRM密鑰伺服器的要求
copied-description: true
exl-id: a5c0db05-15a1-45b0-abb9-11f857f5e34c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# 導言 {#introduction}

黃金時段DRM密鑰伺服器是用於遠程iOS和/或Xbox 360密鑰傳遞的多租戶密鑰伺服器。 如果在iOS的策略中啟用遠程密鑰傳遞，則必須部署黃金時段DRM密鑰伺服器，以便在iOS客戶端上啟用內容回放。 Xbox 360始終需要黃金時段DRM密鑰伺服器。

## 使用黃金時段DRM密鑰伺服器的要求 {#requirements-for-using-primetime-drm-key-server}

使用黃金時段DRM密鑰伺服器的最低要求是：

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 或稍後。 （要在Windows 64位上使用HSM，需要JRE 8）

   >[!NOTE]
   >
   >OpenJDK 8現在支援64位PKCS11: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)和OracleJDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559)。

* [Apache Tomcat 7](https://tomcat.apache.org)
* Adobe頒發的憑據
* Microsoft頒發的憑據（用於Xbox 360客戶端）
