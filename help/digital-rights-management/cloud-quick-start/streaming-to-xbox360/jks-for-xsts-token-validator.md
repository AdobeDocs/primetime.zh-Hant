---
title: 為XSTS驗證程式建立JKS
description: 為XSTS驗證程式建立JKS
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# 為XSTS驗證程式建立JKS{#create-jks-for-an-xsts-validator}

1. 查找位於合作夥伴中的專用證書的別名 [!DNL .pfx] 的子菜單。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 轉換 [!DNL .pfx] 至 [!DNL .jks]。

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   ( `<alias>` 是您在步驟1中發現的專用證書的別名。)
1. 導入 [!DNL x_secure_token_service.part.xboxlive.com.cer]。

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. 放置 [!DNL xsts.jks] 在Tomcat主目錄中，並定義 `-Dxsts-keystore-password=****` 的雙曲餘切值。

如果 [!DNL xsts_partner_cert.pfx] 和 [!DNL xsts.jks] 使用不同的密碼，更新 `xsts` 密碼 `jks` 讓他們變成一樣。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
