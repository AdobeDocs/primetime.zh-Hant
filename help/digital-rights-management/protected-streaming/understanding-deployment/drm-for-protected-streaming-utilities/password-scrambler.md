---
description: Password Scrambler公用程式會加密Adobe Primetime DRM Server的受保護串流設定檔密碼。
seo-description: Password Scrambler公用程式會加密Adobe Primetime DRM Server的受保護串流設定檔密碼。
seo-title: 密碼剪輯器
title: 密碼剪輯器
uuid: 56df0f49-f3fd-464d-b4ba-25e1b497158a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---


# 密碼簽名器{#password-scrambler}

Password Scrambler公用程式會加密Adobe Primetime DRM Server的受保護串流設定檔密碼。

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