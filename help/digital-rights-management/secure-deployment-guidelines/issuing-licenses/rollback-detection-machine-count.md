---
description: 如果業務規則要求跟蹤用戶的電腦數，則許可證伺服器或域伺服器必須儲存與用戶關聯的電腦ID。
title: 核發授權時的機器計數
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# 核發授權{#machine-count-when-issuing-licenses}時的機器計數

如果業務規則要求跟蹤用戶的電腦數，則許可證伺服器或域伺服器必須儲存與用戶關聯的電腦ID。

追蹤機器ID的最強穩方式，是將[MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes())方法傳回的值儲存在資料庫中。 收到新請求時，請使用[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId))，將請求中的機器ID與已知的機器ID進行比較。

[MachineId.matches()會](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 執行ID比較，以判斷ID是否代表相同的機器。只有在機器ID數很少時，此比較才實用。 例如，如果用戶在其域中允許有五台電腦，則可以搜索資料庫中與用戶的用戶名相關聯的電腦ID，並獲取一小組資料以進行比較。

此比較不適用於允許匿名存取的部署。 在此例中，可使用[MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())。 不過，如果使用者從Flash和Adobe AIR®執行階段存取內容，則此ID無法相同。

>[!NOTE]
>
>如果使用者重新格式化硬碟，ID將無法存留。