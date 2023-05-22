---
title: 許可證伺服器配置檔案
description: 許可證伺服器配置檔案
copied-description: true
exl-id: d48e88a4-caae-4f4e-b870-38da4f3a715e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 許可證伺服器配置檔案{#license-server-configuration-files}

用於受保護流的Adobe PrimetimeDRM伺服器需要以下類型的配置檔案：

* 全局配置檔案( [!DNL flashaccess-global.xml])
* 每個租戶的租戶配置檔案( [!DNL flashaccess-tenant.xml])

編輯完配置檔案後，Adobe建議您使用Mogine DRM Server for Protected Streaming隨附的實用程式來驗證檔案格式是否完善。

請參閱 *配置驗證程式*。

如果希望避免在配置檔案中以明文形式提供密碼，則必須使用Adobe提供的Scrambler工具來加密在全局配置檔案和租戶配置檔案中指定的所有密碼。

請參閱 *密碼加擾器* 的子菜單。
