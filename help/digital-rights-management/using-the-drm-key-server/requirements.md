---
title: 使用Primetime DRM Key Server的需求
description: 使用Primetime DRM Key Server的需求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# 簡介{#introduction}

Primetime DRM Key Server是用於遠程iOS和／或Xbox 360金鑰傳送的多租用戶金鑰伺服器。 如果iOS原則中啟用「遠端金鑰傳送」，則必須部署Primetime DRM金鑰伺服器，才能在iOS用戶端上播放內容。 Primetime DRM金鑰伺服器永遠是Xbox 360的必要工具。

## 使用Primetime DRM Key Server {#requirements-for-using-primetime-drm-key-server}的要求

使用Primetime DRM Key Server的最低要求為：

* [Java JRE 1.6或更](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 新版本。（為了在Windows 64位元上使用HSM，需要JRE 8）

   >[!NOTE]
   >
   >OpenJDK 8現在支援64位元PKCS11:[https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)和OracleJDK:[https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559)。

* [Apache Tomcat 7](https://tomcat.apache.org)
* Adobe核發的全權證書
* Microsoft頒發的認證（適用於Xbox 360用戶端）