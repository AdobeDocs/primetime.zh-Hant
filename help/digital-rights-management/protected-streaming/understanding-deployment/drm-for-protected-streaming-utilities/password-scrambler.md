---
description: Password Scrambler公用程式會加密Adobe Primetime DRM Server for Protected Streaming組態檔的密碼。
title: 密碼加擾器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 密碼加擾器 {#password-scrambler}

Password Scrambler公用程式會加密Adobe Primetime DRM Server for Protected Streaming組態檔的密碼。

若要執行擾碼器，請輸入：

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

公用程式會顯示下列訊息：

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

您已在 [!DNL flashaccess-global.xml] 和 [!DNL flashaccess-tenant.xml] 檔案必須加密。

>[!NOTE]
>
>Primetime DRM Server for Protected Streaming中的Password Scrambler公用程式不可與Reference Implementation License Server隨附的Scrambler互換。
