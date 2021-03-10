---
description: SWF雜湊計算器實用程式計算檔案中SWF應用程式的摘要。
title: SWF雜湊計算器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---


# SWF雜湊計算器{#swf-hash-calculator}

SWF雜湊計算器實用程式計算檔案中SWF應用程式的摘要。

要運行散列器，請鍵入：

```
Hasher.bat 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

或

```
java -jar libs/flashaccess-hasher.jar 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

實用程式顯示以下消息：

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

您可以使用此值來指定[!DNL flashaccess-tenant.xml]中的SWF摘要。
