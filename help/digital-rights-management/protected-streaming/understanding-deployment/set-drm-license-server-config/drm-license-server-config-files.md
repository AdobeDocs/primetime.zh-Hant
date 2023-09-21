---
title: 授權伺服器組態檔
description: 授權伺服器組態檔
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 授權伺服器組態檔{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming需要下列型別的組態檔：

* 全域組態檔( [!DNL flashaccess-global.xml])
* 每個租使用者的租使用者設定檔( [!DNL flashaccess-tenant.xml])

完成組態檔的編輯後，Adobe建議您使用Primetime DRM Server for Protected Streaming隨附的公用程式，來確認檔案的格式是否正確。

另請參閱 *設定驗證器*.

如果您想避免在組態檔中以純文字提供密碼，則必須使用Adobe提供的Scrambler工具來加密您在全域和租使用者組態檔中指定的所有密碼。

另請參閱 *密碼加擾器* 以取得如何加密密碼的詳細資訊。
