---
description: flashaccess-global.xml配置檔案包含適用於許可證伺服器的所有租戶的設定。
title: 全局配置檔案
exl-id: 3e74bce6-1634-469f-9d02-1121e9d50687
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 全局配置檔案{#global-configuration-file}

flashaccess-global.xml配置檔案包含適用於許可證伺服器的所有租戶的設定。

必須將配置檔案放在 [!DNL LicenseServer.ConfigRoot] 的子菜單。

查看 [!DNL configs] 的子目錄。

全局配置檔案包括：

* 快取 — 控制記憶體中配置檔案的快取。

   請參閱 *正在更新配置檔案* 的子菜單。
* 日誌記錄 — 指定日誌記錄級別和滾動日誌檔案的頻率。
* HSM密碼 — 僅當使用HSM儲存伺服器憑據時才需要。

請參閱位於Mogife DRM中的示例全局配置檔案中的注釋 `<DVD>`\Adobe Primetime用於受保護流\配置的DRM伺服器瞭解更多詳細資訊。
