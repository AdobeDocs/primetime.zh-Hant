---
title: 正在封裝內容
description: 正在封裝內容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 正在封裝內容{#packaging-content}

封裝內容時，必須指定授權伺服器URL。 Adobe Access Server URL的格式為：

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

例如，對於在連線埠8080上接聽的授權伺服器主機名稱「mylicenseserver.com」和名為「tenant1」的租使用者，封裝時要指定的授權伺服器URL為：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每個租使用者使用不同的License Server和Transport Credential，請務必在封裝器中指定正確的租使用者憑證。

為確保伺服器僅向已知封裝者封裝的內容發行授權，請在封裝者允許租使用者設定檔案清單中包含封裝者的憑證。
