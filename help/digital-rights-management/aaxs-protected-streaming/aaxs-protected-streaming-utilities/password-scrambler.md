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

Password Scrambler公用程式會加密密碼，以便用於Adobe Access Server的Protected Streaming設定檔。 若要執行擾碼器，請執行以下命令：

```
Scrambler.bat password 
```

或命令：

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
>適用於受保護串流的Adobe Access Server中的Password Scrambler公用程式不可與參考實作授權伺服器隨附的Scrambler互換。
