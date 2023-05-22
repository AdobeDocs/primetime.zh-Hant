---
title: 打包內容
description: 打包內容
copied-description: true
exl-id: 85950028-d58d-45b3-9337-9fcabe7cc4c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 打包內容{#packaging-content}

打包內容時，必須指定許可證伺服器URL。 Adobe Access ServerURL的格式為：

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

例如，對於在埠8080上偵聽的許可證伺服器主機名「mylicenseserver.com」和名為「tenant1」的租戶，在打包時要指定的許可證伺服器URL是：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每個租戶使用不同的許可證伺服器和傳輸憑據，請確保在打包器中指定正確的租戶證書。

要確保伺服器僅向由已知打包器打包的內容頒發許可證，請將打包器的證書包括在打包器允許的租戶配置檔案清單中。
