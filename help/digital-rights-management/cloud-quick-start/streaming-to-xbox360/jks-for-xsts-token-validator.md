---
title: 建立XSTS驗證器的JKS
description: 建立XSTS驗證器的JKS
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# 建立XSTS驗證器的JKS{#create-jks-for-an-xsts-validator}

1. 瞭解位於合作夥伴中的私人憑證別名 [!DNL .pfx] 檔案。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 轉換 [!DNL .pfx] 至 [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (其中 `<alias>` 是您在步驟1中發現的私人憑證別名。)
1. 匯入 [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] ，並定義 `-Dxsts-keystore-password=****` 適用於Tomcat。

若 [!DNL xsts_partner_cert.pfx] 和 [!DNL xsts.jks] 使用不同的密碼，請更新 `xsts` 密碼輸入 `jks` 以維持原樣。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
