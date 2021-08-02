---
title: 命令列使用
description: 命令列使用
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# 命令行用法{#command-line-usage}

若要執行工具，請使用下列語法：

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `signaturefile` 指定AIR應用程式signatures.xml檔案的路徑，位於應用程式目 [!DNL META-INF] 錄

* `signingcert` 指定用於簽署AIR應用程式的憑證

>[!NOTE]
>
>若要決定iOS應用程式的發佈者ID，請使用`-s`選項並指定用來簽署iOS應用程式的憑證。 ***Adobe Primetime必須建立可播放存取保護內容的iOS應用程式***。

