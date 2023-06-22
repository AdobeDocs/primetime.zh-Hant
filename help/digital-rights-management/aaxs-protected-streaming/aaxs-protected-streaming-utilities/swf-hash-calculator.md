---
title: SWF雜湊電腦
description: SWF雜湊電腦
copied-description: true
exl-id: 651b31bc-47b5-4388-aa00-27d3bd59da30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# SWF雜湊電腦{#swf-hash-calculator}

SWF雜湊計算器公用程式會計算檔案中SWF應用程式的摘要。 若要執行雜湊程式，請執行以下命令：

```
Hasher.bat filename.swf
```

或命令：

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

公用程式會輸出下列訊息：

```
SWF Hash: hash-of-swf
```

此值可用於指定中的SWF摘要 [!DNL flashaccess-tenant.xml].
