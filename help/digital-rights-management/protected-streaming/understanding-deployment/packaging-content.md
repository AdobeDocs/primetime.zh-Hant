---
description: 在封裝內容時，您必須指定授權伺服器URL。
title: 封裝內容
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# 封裝內容{#packaging-content}

在封裝內容時，您必須指定授權伺服器URL。

Adobe PrimetimeDRM伺服器URL使用下列格式：

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

例如，若是監聽連接埠8080的授權伺服器主機名稱`mylicenseserver.com`，以及名為&#x200B;*`tenant1`*&#x200B;的租用戶，您應針對您封裝內容時所指定的授權伺服器URL使用下列語法：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每個租用戶使用不同的授權伺服器和傳輸憑證，請務必在封裝程式中指定正確的租用戶憑證。

如果您想確定伺服器僅針對已知封裝商的內容發行授權，您必須將封裝商的憑證加入封裝商允許的租用戶設定檔案清單中。
