---
seo-title: 升級客戶端
title: 升級客戶端
uuid: 9c9bc7da-2a97-4659-945a-554d778d30a3
translation-type: tm+mt
source-git-commit: 5cf90a75d8805fb64d7d145722ad10a1ce77a14d
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# 升級客戶端{#upgrading-clients}

如果FMRMS 1.x用戶端連絡Adobe Access伺服器，伺服器需要提示用戶端升級。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 請求URL是&quot;*來自1.x content*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;的基本URL

   與其他Adobe Access請求處理常式不同，此處理常式不提供任何請求資訊的存取權，也不要求設定任何回應資料。 建立`FMRMSv1RequestHandler`的例項，然後呼叫`close()`