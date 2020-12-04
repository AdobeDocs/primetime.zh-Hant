---
seo-title: 許可證伺服器配置檔案
title: 許可證伺服器配置檔案
uuid: 7c7e0f76-2ced-45af-9542-99e06ec31cda
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 許可證伺服器配置檔案{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming需要下列類型的組態檔：

* 全局配置檔案([!DNL flashaccess-global.xml])
* 每個租用戶的租用戶配置檔案([!DNL flashaccess-tenant.xml])

在您完成設定檔的編輯後，Adobe建議您使用Primetime DRM Server for Protected Streaming隨附的公用程式，以確認檔案格式正確。

請參閱&#x200B;*Configuration Validator*。

如果您不想讓設定檔案中的密碼以明文提供，則必須使用Adobe提供的Scrambler工具，加密您在全域和租用戶設定檔案中指定的所有密碼。

有關如何加密密碼的詳細資訊，請參見&#x200B;*密碼刪除程式*。
