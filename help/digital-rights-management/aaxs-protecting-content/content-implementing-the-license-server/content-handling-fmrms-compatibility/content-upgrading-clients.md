---
title: 升級客戶端
description: 升級客戶端
copied-description: true
exl-id: 0476c9ef-3622-4bc5-bb24-f8543470b7d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 升級客戶端{#upgrading-clients}

如果FMRMS 1.x客戶端與Adobe訪問伺服器聯繫，則伺服器需要提示客戶端進行升級。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 請求URL為「」*1.x內容的基URL*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   與其他Adobe訪問請求處理程式不同，此處理程式不提供對任何請求資訊的訪問，也不要求設定任何響應資料。 建立實例 `FMRMSv1RequestHandler`，然後調用 `close()`
