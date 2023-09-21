---
description: 當您封裝內容時，必須指定許可證伺服器URL。
title: 正在封裝內容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 正在封裝內容{#packaging-content}

當您封裝內容時，必須指定許可證伺服器URL。

Adobe Primetime DRM伺服器URL會使用以下格式：

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

例如，對於許可證伺服器主機名稱 `mylicenseserver.com` 接聽連線埠8080的租使用者，名為 *`tenant1`*，您會針對封裝內容時指定的許可證伺服器URL使用下列語法：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每個租使用者使用不同的License Server和Transport Credential，請務必在封裝器中指定正確的租使用者憑證。

如果您想要確定伺服器僅向來自已知封裝者的內容發行授權，您必須在封裝者允許租使用者設定檔案清單中包含封裝者的憑證。
