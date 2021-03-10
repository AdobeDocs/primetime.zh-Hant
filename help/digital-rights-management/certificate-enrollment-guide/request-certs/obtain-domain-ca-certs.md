---
title: 獲取域CA證書
description: 獲取域CA證書
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# 獲取域CA證書{#obtain-domain-ca-certificates}

與License Server、Packager或Transport證書不同，域CA證書不由Adobe頒發。 您可從認證機構取得此憑證，或產生自行簽署的憑證以用於此用途。

域CA證書應使用1024位密鑰，並包含CA證書中所需的標準屬性：

* CA標幟設為true時的基本約束擴充功能
* 允許使用金鑰擴充功能指定憑證簽署

例如，使用OpenSSL，可以產生自簽名的CA憑證，如下所示：

1. 建立名為[!DNL ca-extensions.txt]的檔案，其中包含：

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. 產生金鑰：

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. 生成CSR:

   ```
   openssl req -new -key domain-ca.key -out domain-ca.csr 
   ```

1. 產生憑證：

   ```
   openssl x509 -req -days 365 -in domain-ca.csr -signkey domain-ca.key \ 
     -out domain-ca.cer -extfile ca-extensions.txt 
   ```

1. 產生密碼：

   ```
   openssl rand -base64 8 
   ```

1. 產生PFX:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```

