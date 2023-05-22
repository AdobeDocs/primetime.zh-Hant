---
description: 打包內容時，必須指定許可證伺服器URL。
title: 打包內容
exl-id: f82385d5-cdb3-4c24-822e-3fc3c3a0793f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 打包內容{#packaging-content}

打包內容時，必須指定許可證伺服器URL。

Adobe PrimetimeDRM伺服器URL使用以下格式：

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

例如，對於許可證伺服器主機名 `mylicenseserver.com` 在8080埠監聽，租戶叫 *`tenant1`*，您將在打包內容時指定的許可證伺服器URL使用以下語法：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每個租戶使用不同的許可證伺服器和傳輸憑據，請確保在打包器中指定正確的租戶證書。

如果要確保伺服器僅向已知打包機的內容頒發許可證，則需要在打包機允許租戶配置檔案清單中包括打包機的證書。
