---
title: 密碼加擾器
description: 密碼加擾器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# 密碼加擾器 {#password-scrambler}

密碼擾碼器公用程式會加密密碼，以便用於Adobe Access Server的Protected Streaming設定檔。 若要執行擾碼器，請執行以下命令：

```
Scrambler.bat password 
```

或指令：

```
java -jar libs/flashaccess-scrambler.jar password  
```

公用程式輸出下列訊息：

```
Encrypted password: scrambled-password 
```

flashaccess-global.xml和flashaccess-tenant.xml中指定的所有密碼都必須加密。

>[!NOTE]
>
>在Adobe Access Server中，Protected Streaming的Password Scrambler公用程式不可與Reference Implementation License Server隨附的Scrambler互換。
