---
title: 升級Adobe Primetime DRM伺服器以使用受保護的資料流
description: 升級Adobe Primetime DRM伺服器以使用受保護的資料流
copied-description: true
exl-id: 6edfba1b-46a2-4cbd-bc14-feeef1a36ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 升級Adobe Primetime DRM伺服器以使用受保護的資料流{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

如果您想要升級執行Primetime DRM伺服器以進行受保護串流的伺服器，您需要將 `flashaccessserver.war` 已使用隨最新Primetime DRM附帶的檔案部署在應用程式伺服器上的檔案。

如果您想要使用新的設定選項，您需要更新伺服器的 `flashaccess-tenant.xml`. 您也需要更新 [!DNL jsafe.dll] 或 [!DNL libjsafe.so] 隨附於最新Primetime DRM的版本。
