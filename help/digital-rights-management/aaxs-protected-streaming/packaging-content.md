---
title: 封裝內容
description: 封裝內容
copied-description: true
exl-id: 85950028-d58d-45b3-9337-9fcabe7cc4c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 封裝內容{#packaging-content}

封裝內容時，必須指定授權伺服器URL。 Adobe Access Server URL的格式為：

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

例如，對於在連線埠8080上接聽的授權伺服器主機名稱「mylicenseserver.com」和名為「tenant1」的租使用者，封裝時要指定的授權伺服器URL是：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每個租使用者使用不同的授權伺服器和傳輸認證，請務必在封裝器中指定正確的租使用者憑證。

為確保伺服器僅向已知封裝者封裝的內容發行授權，請在封裝者允許租使用者設定檔案清單中納入封裝者的憑證。
