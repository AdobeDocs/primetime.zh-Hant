---
seo-title: 密碼剪貼器
title: 密碼剪貼器
uuid: e488babc-cd50-41b9-acb8-490e8e42e8bc
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# 密碼刪除程式{#password-scrambler}

Password Scrambler公用程式會加密密碼，以便用於Adobe Access Server for Protected Streaming設定檔。 要運行scrambler，請運行命令：

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

Flashaccess-global.xml和flashaccess-tenant.xml中指定的所有密碼都必須加密。

>[!NOTE]
>
>Adobe Access Server中用於受保護串流的密碼剪貼程式公用程式無法與參考實施授權伺服器隨附的剪貼程式互換。

