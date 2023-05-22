---
title: 升級Adobe PrimetimeDRM伺服器以進行受保護的流處理
description: 升級Adobe PrimetimeDRM伺服器以進行受保護的流處理
copied-description: true
exl-id: 6edfba1b-46a2-4cbd-bc14-feeef1a36ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 升級Adobe PrimetimeDRM伺服器以進行受保護的流處理{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

如果要升級運行Mogfire DRM Server for Protected Streaming的伺服器，需要替換 `flashaccessserver.war` 已部署在應用程式伺服器上且最新Mogfire DRM包含的檔案的檔案。

如果要使用新的配置選項，則需要更新伺服器 `flashaccess-tenant.xml`。 您還需要更新 [!DNL jsafe.dll] 或 [!DNL libjsafe.so] 最新黃金時段DRM中包含的版本。
