---
title: 使用Primetime DRM金鑰伺服器的需求
description: 使用Primetime DRM金鑰伺服器的需求
copied-description: true
exl-id: a5c0db05-15a1-45b0-abb9-11f857f5e34c
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 簡介 {#introduction}

Primetime DRM Key Server是用於遠端iOS和/或Xbox 360金鑰傳遞的多租使用者金鑰伺服器。 如果在iOS的原則中啟用了遠端金鑰傳遞，則必須部署Primetime DRM金鑰伺服器，才能在iOS使用者端上啟用內容播放。 Xbox 360一律需要Primetime DRM金鑰伺服器。

## 使用Primetime DRM金鑰伺服器的需求 {#requirements-for-using-primetime-drm-key-server}

使用Primetime DRM Key Server的最低需求為：

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 或更新版本。 （若要在Windows 64位元上使用HSM，需要JRE 8）

  >[!NOTE]
  >
  >OpenJDK 8現在支援64位元PKCS11： [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)，和Oracle
* [Apache Tomcat 7](https://tomcat.apache.org)
* 由Adobe簽發的認證
* Microsoft核發的認證（適用於Xbox 360使用者端）
