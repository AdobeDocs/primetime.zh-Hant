---
description: 封裝內容時，您必須指定授權伺服器URL。
title: 封裝內容
exl-id: f82385d5-cdb3-4c24-822e-3fc3c3a0793f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 封裝內容{#packaging-content}

封裝內容時，您必須指定授權伺服器URL。

Adobe Primetime DRM伺服器URL會使用以下格式：

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

例如，對於授權伺服器主機名稱 `mylicenseserver.com` 接聽連線埠8080和名為的租使用者的伺服器 *`tenant1`*，您會針對封裝內容時指定的授權伺服器URL使用下列語法：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每個租使用者使用不同的授權伺服器和傳輸認證，請務必在封裝程式中指定正確的租使用者憑證。

如果您想要確保伺服器僅向來自已知封裝者的內容發行授權，您需要將封裝者的憑證包含在封裝者允許租使用者設定檔案的清單中。
