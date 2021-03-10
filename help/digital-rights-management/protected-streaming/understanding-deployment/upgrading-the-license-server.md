---
title: 升級Adobe PrimetimeDRM Server以進行受保護的串流
description: 升級Adobe PrimetimeDRM Server以進行受保護的串流
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 升級Adobe PrimetimeDRM Server for Protected Streaming{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

如果您想要升級執行Primetime DRM Server for Protected Streaming的伺服器，您需要將已部署在應用程式伺服器上的`flashaccessserver.war`檔案取代為最新Primetime DRM所包含的檔案。

如果要使用新的配置選項，則需要更新伺服器的`flashaccess-tenant.xml`。 此外，您還需要更新[!DNL jsafe.dll]或[!DNL libjsafe.so]的最新Primetime DRM版本。
