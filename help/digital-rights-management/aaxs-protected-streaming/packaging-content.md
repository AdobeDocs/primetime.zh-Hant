---
seo-title: 封裝內容
title: 封裝內容
uuid: 5d1d4b9d-f241-4291-9577-e9de5a8b92be
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# 封裝內容{#packaging-content}

封裝內容時，必須指定授權伺服器URL。 Adobe Access Server URL的格式如下：

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

例如，若是在連接埠8080上監聽授權伺服器主機名稱&quot;mylicenseserver.com&quot;和名為&quot;tenant1&quot;的租用戶，在封裝時要指定的授權伺服器URL為：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每個租用戶使用不同的授權伺服器和傳輸憑證，請務必在封裝程式中指定正確的租用戶憑證。

為確保伺服器僅向已知打包員打包的內容發放許可證，請將打包員的證書包括在租用戶配置檔案的打包員白名單中。
