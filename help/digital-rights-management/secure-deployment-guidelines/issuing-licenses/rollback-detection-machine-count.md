---
description: 如果商業規則要求追蹤使用者的電腦數目，則License Server或Domain Server必須儲存與使用者相關聯的電腦ID。
title: 簽發授權時的電腦計數
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# 簽發授權時的電腦計數 {#machine-count-when-issuing-licenses}

如果商業規則要求追蹤使用者的電腦數目，則License Server或Domain Server必須儲存與使用者相關聯的電腦ID。

追蹤機器ID最有效的方法是儲存 [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 方法。 收到新請求時，請使用將請求中的電腦ID與已知的電腦ID進行比較 [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 會執行ID的比較，以判斷ID是否代表同一部電腦。 只有少數電腦ID時，此比較才切實可行。 例如，如果使用者在其網域中允許使用五台電腦，您可以在資料庫中搜尋與使用者使用者名稱相關聯的電腦ID，並取得一小部分資料集以進行比較。

此比較不適用於允許匿名存取的部署。 在這種情況下， [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 可使用。 但是，如果使用者從Flash和Adobe AIR®執行階段存取內容，則此ID不能相同。

>[!NOTE]
>
>如果使用者重新格式化硬碟，該ID將無法存留。