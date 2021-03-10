---
title: 密碼剪貼器
description: 密碼剪貼器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# 密碼刪除程式{#password-scrambler}

Password Scrambler實用程式會加密密碼，以便用於Adobe Access Server的受保護流配置檔案。 要運行scrambler，請運行命令：

```
Scrambler.bat password 
```

或命令：

```
java -jar libs/flashaccess-scrambler.jar password  
```

實用程式輸出以下消息：

```
Encrypted password: scrambled-password 
```

在flashaccess-global.xml和flashaccess-tenant.xml中指定的所有密碼都必須加密。

>[!NOTE]
>
>Adobe Access Server保護串流的密碼剪輯器公用程式無法與隨參考實施授權伺服器提供的剪輯器互換。

