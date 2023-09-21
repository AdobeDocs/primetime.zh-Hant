---
title: 取得網域CA憑證
description: 取得網域CA憑證
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 取得網域CA憑證{#obtain-domain-ca-certificates}

與License Server、Packager或Transport憑證不同，網域CA憑證不是由Adobe所簽發。 您可以從憑證授權單位取得此憑證，也可以產生自我簽署憑證以用於此用途。

網域CA憑證應使用1024位元金鑰，並包含CA憑證所需的標準屬性：

* CA標幟設為True的基本限制延伸
* 指定憑證簽章的金鑰使用延伸是允許的

例如，使用OpenSSL，可以產生自我簽署CA憑證，如下所示：

1. 建立名為的檔案 [!DNL ca-extensions.txt] 包含：

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. 產生金鑰：

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. 產生CSR：

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

1. 產生PFX：

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```
