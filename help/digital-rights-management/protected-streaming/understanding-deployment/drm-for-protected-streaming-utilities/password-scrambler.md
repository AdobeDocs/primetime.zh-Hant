---
description: Password Scrambler實用程式加密Adobe PrimetimeDRM伺服器的受保護流配置檔案的密碼。
title: 密碼剪輯器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 密碼簽字器{#password-scrambler}

Password Scrambler實用程式加密Adobe PrimetimeDRM伺服器的受保護流配置檔案的密碼。

若要執行剪貼簿，請輸入：

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

或

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

實用程式顯示以下消息：

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

您在[!DNL flashaccess-global.xml]和[!DNL flashaccess-tenant.xml]檔案中指定的所有密碼都必須加密。

>[!NOTE]
>
>用於受保護流的Primetime DRM伺服器中的密碼擾碼器實用程式不能與隨參考實施許可證伺服器提供的擾碼器互換。