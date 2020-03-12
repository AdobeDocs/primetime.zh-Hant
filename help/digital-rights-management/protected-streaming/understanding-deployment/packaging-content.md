---
description: 在封裝內容時，您必須指定授權伺服器URL。
seo-description: 在封裝內容時，您必須指定授權伺服器URL。
seo-title: 封裝內容
title: 封裝內容
uuid: 2e47a9a2-bbc6-4995-8ce5-6ca6b116349b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 封裝內容{#packaging-content}

在封裝內容時，您必須指定授權伺服器URL。

Adobe Primetime DRM Server URL使用下列格式：

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

例如，若是監聽連接埠8080 `mylicenseserver.com` 的授權伺服器主機名稱，以及呼叫租用戶 *`tenant1`*，您應針對您封裝內容時所指定的授權伺服器URL使用下列語法：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每個租用戶使用不同的授權伺服器和傳輸憑證，請務必在封裝程式中指定正確的租用戶憑證。

如果您想確定伺服器僅針對已知封裝商的內容發行授權，您必須將封裝商的憑證加入租用戶設定檔案的封裝商白名單中。
