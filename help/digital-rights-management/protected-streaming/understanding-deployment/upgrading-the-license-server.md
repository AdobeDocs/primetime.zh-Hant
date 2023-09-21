---
title: 升級Adobe Primetime DRM伺服器以使用受保護的串流
description: 升級Adobe Primetime DRM伺服器以使用受保護的串流
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 升級Adobe Primetime DRM伺服器以使用受保護的串流{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

如果您想要升級執行Primetime DRM Server for Protected Streaming的伺服器，您需要將 `flashaccessserver.war` 已部署在應用程式伺服器上的檔案，其檔案已包含在最新的Primetime DRM中。

如果您想要使用新的組態選項，則需要更新伺服器的 `flashaccess-tenant.xml`. 您也需要更新 [!DNL jsafe.dll] 或 [!DNL libjsafe.so] 與最新的Primetime DRM隨附的版本一起使用。
