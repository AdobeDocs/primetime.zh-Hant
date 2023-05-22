---
description: SDK定期下載由Adobe發佈的CRL。 必須確保不阻止對這些檔案的訪問或不阻止對這些CRL的強制執行。
title: 正在使用Adobe發佈的CRL
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 正在使用Adobe發佈的CRL{#consuming-crls-published-by-adobe}

SDK定期下載由Adobe發佈的CRL。 必須確保不阻止對這些檔案的訪問或不阻止對這些CRL的強制執行。

SDK具有一個配置選項，可以在檢索AdobeCRL時忽略錯誤，並且您只能在開發環境中應用此選項。 在生產環境中，許可證伺服器必須從Adobe中檢索CRL。 如果許可證伺服器無法獲取有效的CRL，則發生錯誤。
