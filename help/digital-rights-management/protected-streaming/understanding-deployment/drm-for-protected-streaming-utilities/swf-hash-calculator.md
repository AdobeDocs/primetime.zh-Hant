---
description: SWF雜湊計算器公用程式會計算檔案中SWF應用程式的摘要。
title: SWF雜湊計算器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# SWF雜湊計算器{#swf-hash-calculator}

SWF雜湊計算器公用程式會計算檔案中SWF應用程式的摘要。

若要執行雜湊程式，請輸入：

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

公用程式會顯示下列訊息：

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

您可以使用此值來指定中的SWF摘要 [!DNL flashaccess-tenant.xml].
