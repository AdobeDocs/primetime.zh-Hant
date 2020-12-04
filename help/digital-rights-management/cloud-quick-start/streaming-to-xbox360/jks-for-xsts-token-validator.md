---
seo-title: 為XSTS驗證器建立JKS
title: 為XSTS驗證器建立JKS
uuid: e02b517d-0b72-4e95-92b2-09b8f785cce6
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# 為XSTS驗證器建立JKS{#create-jks-for-an-xsts-validator}

1. 查找位於夥伴[!DNL .pfx]檔案中的私有證書的別名。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 將[!DNL .pfx]轉換為[!DNL .jks]。

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   （其中`<alias>`是您在步驟1中發現的私有證書別名）。
1. 導入[!DNL x_secure_token_service.part.xboxlive.com.cer]。

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. 將[!DNL xsts.jks]放在Tomcat主目錄中，並定義Tomcat的`-Dxsts-keystore-password=****`。

如果[!DNL xsts_partner_cert.pfx]和[!DNL xsts.jks]使用不同的密碼，請更新`jks`中的`xsts`密碼，使其相同。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
