---
title: 全局配置檔案
description: 全局配置檔案
copied-description: true
exl-id: 5a2f96fe-d39d-4391-a010-200a900b043b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 全局配置檔案{#global-configuration-file}

flashaccess-global.xml配置檔案包含適用於許可證伺服器的所有租戶的設定。 此檔案必須位於 *LicenseServer.ConfigRoot*。 有關全局配置檔案的示例，請參見configs目錄。 全局配置檔案包括以下內容：

* 快取 — 控制記憶體中配置檔案的快取。 有關快取設定的說明，請參閱更新配置檔案。
* 日誌記錄 — 指定日誌記錄級別和滾動日誌檔案的頻率。
* HSM密碼 — 僅當使用HSM儲存伺服器憑據時才需要。

請參閱位於 `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` 的子菜單。
