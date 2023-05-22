---
title: 使用由Adobe發佈的CRL
description: 使用由Adobe發佈的CRL
copied-description: true
exl-id: b7f68a29-f834-4613-b64d-e610f660e6fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 使用由Adobe發佈的CRL{#consume-crls-published-by-adobe}

SDK定期下載由Adobe發佈的CRL。 不要阻止對這些檔案的訪問或阻止對這些CRL的強制執行。

SDK具有一個配置選項，可在檢索AdobeCRL時忽略錯誤。 此選項只能用於開發環境。 在生產環境中，許可證伺服器必須能夠從Adobe中檢索CRL。 無法獲取有效CRL是錯誤。
