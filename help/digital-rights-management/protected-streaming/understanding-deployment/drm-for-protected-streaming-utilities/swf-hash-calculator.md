---
description: 「SWF雜湊電腦」公用程式會計算位於檔案中的SWF應用程式的摘要。
title: SWF雜湊電腦
exl-id: 245254fe-2fcb-41e8-94bd-0cbc8b39b2b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# SWF雜湊電腦{#swf-hash-calculator}

「SWF雜湊電腦」公用程式會計算位於檔案中的SWF應用程式的摘要。

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

您可以使用此值來指定SWF摘要，在 [!DNL flashaccess-tenant.xml].
