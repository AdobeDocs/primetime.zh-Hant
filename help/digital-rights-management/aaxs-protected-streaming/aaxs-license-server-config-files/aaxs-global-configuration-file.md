---
title: 全局配置檔案
description: 全局配置檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# 全局配置檔案{#global-configuration-file}

flashaccess-global.xml設定檔包含適用於授權伺服器所有租戶的設定。 此檔案必須位於&#x200B;*LicenseServer.ConfigRoot*&#x200B;中。 有關全局配置檔案示例，請參見configs目錄。 全域設定檔包含下列項目：

* 快取— 控制記憶體中配置檔案的快取。 如需快取設定的說明，請參閱「更新設定檔」。
* 記錄— 指定記錄級別以及記錄檔案的滾動頻率。
* HSM密碼— 僅當使用HSM儲存伺服器憑據時才需要。

如需詳細資訊，請參閱位於`<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs`的範例全域設定檔案中的注釋。
