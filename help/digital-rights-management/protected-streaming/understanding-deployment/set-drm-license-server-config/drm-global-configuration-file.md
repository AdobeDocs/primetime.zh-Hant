---
description: flashaccess-global.xml組態檔包含套用至授權伺服器所有租使用者的設定。
title: 全域設定檔
exl-id: 3e74bce6-1634-469f-9d02-1121e9d50687
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 全域設定檔{#global-configuration-file}

flashaccess-global.xml組態檔包含套用至授權伺服器所有租使用者的設定。

您必須將設定檔案放入 [!DNL LicenseServer.ConfigRoot] 目錄。

請參閱 [!DNL configs] 目錄，以取得全域組態檔的範例。

全域組態檔包含：

* 快取 — 控制記憶體中組態檔案的快取。

   另請參閱 *更新組態檔* 以取得快取設定的相關資訊。
* 記錄 — 指定記錄層級以及記錄檔的捲動頻率。
* HSM密碼 — 只有在使用HSM儲存伺服器憑證時才需要。

請參閱位於Primetime DRM中的範例全域組態檔案中的註解 `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs以取得詳細資訊。
