---
description: 如果業務規則要求跟蹤用戶的電腦數，則許可證伺服器或域伺服器必須儲存與用戶關聯的電腦ID。
title: 頒發許可證時的電腦計數
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# 頒發許可證時的電腦計數 {#machine-count-when-issuing-licenses}

如果業務規則要求跟蹤用戶的電腦數，則許可證伺服器或域伺服器必須儲存與用戶關聯的電腦ID。

跟蹤電腦ID的最穩健方法是儲存由 [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 中的設定。 收到新請求後，使用 [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId))。

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 執行ID的比較以確定ID是否代表同一台電腦。 此比較僅在有少量電腦ID時才實用。 例如，如果允許用戶在其域中使用五台電腦，則可以在資料庫中搜索與用戶用戶名關聯的電腦ID，並獲取一小組資料以供比較。

此比較對於允許匿名訪問的部署不實用。 在這個例子中， [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 可使用。 但是，如果用戶從Flash和Adobe AIR®運行時訪問內容，則此ID不能相同。

>[!NOTE]
>
>如果用戶重新格式化硬碟，ID將無法存在。