---
description: flashaccess-global.xml組態檔包含套用至許可證伺服器所有租使用者的設定。
title: 全域設定檔
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 全域設定檔{#global-configuration-file}

flashaccess-global.xml組態檔包含套用至許可證伺服器所有租使用者的設定。

您必須將組態檔案放在 [!DNL LicenseServer.ConfigRoot] 目錄。

請參閱 [!DNL configs] 目錄，作為全域組態檔的範例。

全域組態檔包含：

* 快取 — 控制記憶體中組態檔案的快取。

  另請參閱 *正在更新組態檔* 以取得快取設定的相關資訊。
* 記錄 — 指定記錄層級和記錄檔的捲動頻率。
* HSM密碼 — 只有在使用HSM儲存伺服器憑證時才需要。

請參閱位於Primetime DRM中的範例全域組態檔案中的註解 `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs以取得詳細資訊。
