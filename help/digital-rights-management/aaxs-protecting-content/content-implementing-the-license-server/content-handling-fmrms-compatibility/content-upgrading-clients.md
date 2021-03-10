---
title: 升級客戶端
description: 升級客戶端
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# 升級客戶端{#upgrading-clients}

如果FMRMS 1.x客戶端與Adobe訪問伺服器聯繫，則伺服器需要提示客戶端升級。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 請求URL是&quot;*來自1.x content*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;的基本URL

   與其他Adobe訪問請求處理程式不同，此處理程式不提供對任何請求資訊的訪問，也不要求設定任何響應資料。 建立`FMRMSv1RequestHandler`的例項，然後呼叫`close()`