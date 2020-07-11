---
seo-title: 封裝內容
title: 封裝內容
uuid: 5d1d4b9d-f241-4291-9577-e9de5a8b92be
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

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

為確保伺服器僅向已知打包員打包的內容發放許可證，請將打包員的證書包括在包裝員允許的租用戶配置檔案清單中。
