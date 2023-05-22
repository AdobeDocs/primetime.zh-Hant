---
title: 密碼加擾器
description: 密碼加擾器
copied-description: true
exl-id: ceedd61e-918b-453f-8d21-628b2d8713ff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# 密碼加擾器 {#password-scrambler}

密碼加擾器實用程式加密密碼，以便在Adobe Access Server中用於受保護流配置檔案。 要運行擾碼器，請運行以下命令：

```
Scrambler.bat password 
```

或命令：

```
java -jar libs/flashaccess-scrambler.jar password  
```

該實用程式輸出以下消息：

```
Encrypted password: scrambled-password 
```

必須加密flashaccess-global.xml和flashaccess-tenant.xml中指定的所有密碼。

>[!NOTE]
>
>Adobe Access Server保護流的密碼加擾器實用程式不能與隨參考實施許可證伺服器提供的加擾器互換。
