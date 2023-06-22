---
description: Password Scrambler公用程式會加密Adobe Primetime DRM伺服器的Protected Streaming組態檔密碼。
title: 密碼加擾器
exl-id: 9cedd3e5-01db-4ea9-bf23-8767987fc26c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 密碼加擾器 {#password-scrambler}

Password Scrambler公用程式會加密Adobe Primetime DRM伺服器的Protected Streaming組態檔密碼。

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

您指定的所有密碼 [!DNL flashaccess-global.xml] 和 [!DNL flashaccess-tenant.xml] 檔案必須加密。

>[!NOTE]
>
>Primetime DRM Server for Protected Streaming中的Password Scrambler公用程式不可與Reference Implementation License Server隨附的Scrambler交換。
