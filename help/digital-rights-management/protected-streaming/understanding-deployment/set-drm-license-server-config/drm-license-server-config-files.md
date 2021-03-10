---
title: 許可證伺服器配置檔案
description: 許可證伺服器配置檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 許可證伺服器配置檔案{#license-server-configuration-files}

Adobe PrimetimeDRM Server for Protected Streaming需要以下類型的配置檔案：

* 全局配置檔案([!DNL flashaccess-global.xml])
* 每個租用戶的租用戶配置檔案([!DNL flashaccess-tenant.xml])

完成配置檔案編輯後，Adobe建議您使用Primetime DRM Server for Protected Streaming隨附的實用程式來驗證檔案的格式是否正確。

請參閱&#x200B;*Configuration Validator*。

如果您不想讓設定檔案中的密碼以明文提供，則必須使用Adobe提供的Scrambler工具，來加密您在全域和租用戶設定檔案中指定的所有密碼。

有關如何加密密碼的詳細資訊，請參見&#x200B;*密碼刪除程式*。
