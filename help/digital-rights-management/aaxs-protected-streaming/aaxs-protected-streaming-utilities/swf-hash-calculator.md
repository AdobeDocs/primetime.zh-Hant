---
title: SWF哈希計算器
description: SWF哈希計算器
copied-description: true
exl-id: 651b31bc-47b5-4388-aa00-27d3bd59da30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# SWF哈希計算器{#swf-hash-calculator}

SWF哈希計算器實用程式計算位於檔案中的SWF應用程式的摘要。 要運行哈希器，請運行命令：

```
Hasher.bat filename.swf
```

或命令：

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

該實用程式輸出以下消息：

```
SWF Hash: hash-of-swf
```

此值可用於指定中的SWF摘要 [!DNL flashaccess-tenant.xml]。
