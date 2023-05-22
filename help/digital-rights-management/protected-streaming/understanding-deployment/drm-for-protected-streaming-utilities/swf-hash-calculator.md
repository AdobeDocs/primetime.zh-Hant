---
description: SWF哈希計算器實用程式計算位於檔案中的SWF應用程式的摘要。
title: SWF哈希計算器
exl-id: 245254fe-2fcb-41e8-94bd-0cbc8b39b2b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# SWF哈希計算器{#swf-hash-calculator}

SWF哈希計算器實用程式計算位於檔案中的SWF應用程式的摘要。

要運行哈希器，請鍵入：

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

可以使用此值指定中的SWF摘要 [!DNL flashaccess-tenant.xml]。
