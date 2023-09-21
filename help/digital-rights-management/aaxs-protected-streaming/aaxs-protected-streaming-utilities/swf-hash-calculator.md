---
title: SWF雜湊電腦
description: SWF雜湊電腦
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# SWF雜湊電腦{#swf-hash-calculator}

SWF雜湊計算器公用程式計算檔案中SWF應用程式的摘要。 若要執行雜湊程式，請執行以下命令：

```
Hasher.bat filename.swf
```

或指令：

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

公用程式輸出下列訊息：

```
SWF Hash: hash-of-swf
```

此值可用於指定中的SWF摘要 [!DNL flashaccess-tenant.xml].
