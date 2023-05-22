---
title: 獲取域CA證書
description: 獲取域CA證書
copied-description: true
exl-id: cad233e0-41f7-4897-ab5f-d5a098c37306
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 獲取域CA證書{#obtain-domain-ca-certificates}

與許可證伺服器、打包程式或傳輸證書不同，域CA證書不是由Adobe頒發的。 您可以從證書頒發機構獲取此證書，或者可以生成用於此目的的自簽名證書。

域CA證書應使用1024位密鑰，並包含CA證書中所需的標準屬性：

* CA標誌設定為true時的基本約束擴展
* 允許指定證書籤名的密鑰使用擴展

例如，使用OpenSSL，可以按如下方式生成自簽名CA證書：

1. 建立名為 [!DNL ca-extensions.txt] 包含：

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. 生成密鑰：

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. 生成CSR:

   ```
   openssl req -new -key domain-ca.key -out domain-ca.csr 
   ```

1. 生成證書：

   ```
   openssl x509 -req -days 365 -in domain-ca.csr -signkey domain-ca.key \ 
     -out domain-ca.cer -extfile ca-extensions.txt 
   ```

1. 生成密碼：

   ```
   openssl rand -base64 8 
   ```

1. 生成PFX:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```
