---
seo-title: SWF雜湊計算器
title: SWF雜湊計算器
uuid: c1823208-92d9-47c5-b550-f9cc370b543d
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
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
