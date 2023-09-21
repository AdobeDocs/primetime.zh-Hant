---
title: 命令列使用方式
description: 命令列使用方式
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 命令列使用方式 {#command-line-usage}

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

* `signaturefile` 指定AIR應用程式signatures.xml檔案（位於應用程式中）的路徑 [!DNL META-INF] 目錄

* `signingcert` 指定用於簽署AIR應用程式的憑證

>[!NOTE]
>
>若要判斷iOS應用程式的發佈者ID，請使用 `-s` 選項並指定用來簽署iOS應用程式的憑證。 ***建置可以播放受存取保護內容的iOS應用程式需要Adobe Primetime***.
