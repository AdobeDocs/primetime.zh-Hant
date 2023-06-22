---
title: 授權伺服器組態檔
description: 授權伺服器組態檔
copied-description: true
exl-id: d48e88a4-caae-4f4e-b870-38da4f3a715e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 授權伺服器組態檔{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming需要下列型別的組態檔：

* 全域組態檔( [!DNL flashaccess-global.xml])
* 每個租使用者的租使用者設定檔( [!DNL flashaccess-tenant.xml])

完成編輯組態檔案後，Adobe建議您使用Primetime DRM伺服器隨附的公用程式來驗證檔案的格式是否正確。

另請參閱 *設定驗證器*.

如果您不想在設定檔案中以純文字提供密碼，則必須使用Adobe提供的Scrambler工具來加密您在全域和租使用者設定檔案中指定的所有密碼。

另請參閱 *密碼加擾器* 以取得如何加密密碼的詳細資訊。
