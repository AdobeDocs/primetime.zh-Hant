---
title: 全域設定檔
description: 全域設定檔
copied-description: true
exl-id: 5a2f96fe-d39d-4391-a010-200a900b043b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 全域設定檔{#global-configuration-file}

flashaccess-global.xml組態檔包含套用至授權伺服器所有租使用者的設定。 此檔案必須位於 *LicenseServer.ConfigRoot*. 如需範例全域組態檔，請參閱configs目錄。 全域組態檔包含下列內容：

* 快取 — 控制記憶體中組態檔案的快取。 如需快取設定的說明，請參閱更新組態檔。
* 記錄 — 指定記錄層級以及記錄檔的捲動頻率。
* HSM密碼 — 只有在使用HSM儲存伺服器憑證時才需要。

請參閱位於下列位置的範例全域組態檔中的註解： `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` 以取得更多詳細資料。
