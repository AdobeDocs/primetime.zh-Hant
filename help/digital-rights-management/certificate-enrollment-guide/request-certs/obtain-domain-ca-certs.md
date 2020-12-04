---
seo-title: 獲取域CA證書
title: 獲取域CA證書
uuid: 41bbe02b-363a-47f4-9cc0-350730b6c787
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# 獲取域CA證書{#obtain-domain-ca-certificates}

與「授權伺服器」、「封裝器」或「傳輸」憑證不同，網域CA憑證不是由Adobe核發。 您可從認證機構取得此憑證，或產生自行簽署的憑證以用於此用途。

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

