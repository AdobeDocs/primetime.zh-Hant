---
title: SWF雜湊計算器
description: SWF雜湊計算器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# SWF雜湊計算器{#swf-hash-calculator}

SWF雜湊計算器實用程式計算檔案中SWF應用程式的摘要。 要運行hasher，請運行命令：

```
Hasher.bat filename.swf
```

或命令：

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

實用程式輸出以下消息：

```
SWF Hash: hash-of-swf
```

此值可用於指定[!DNL flashaccess-tenant.xml]中的SWF摘要。
