---
title: 升級使用者端
description: 升級使用者端
copied-description: true
exl-id: 0476c9ef-3622-4bc5-bb24-f8543470b7d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 升級使用者端{#upgrading-clients}

如果FMRMS 1.x使用者端連絡Adobe存取伺服器，伺服器必須提示使用者端進行升級。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* 請求URL是&quot;*來自1.x內容的基礎URL*&quot; + &quot;/edcws/services/urn：EDCLicenseService&quot;

   與其他Adobe存取要求處理常式不同，此處理常式不會提供任何要求資訊的存取權，或要求設定任何回應資料。 建立的執行個體 `FMRMSv1RequestHandler`，然後呼叫 `close()`
