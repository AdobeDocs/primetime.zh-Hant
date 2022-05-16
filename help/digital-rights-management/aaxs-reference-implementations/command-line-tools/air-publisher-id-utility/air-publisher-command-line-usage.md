---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 67056085-beb5-4f54-8962-369bc32d7907
source-git-commit: 79cab347d0daa01549fbf8a9b37bf0a91c14648e
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

要運行該工具，請使用以下語法：

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

* `signaturefile` 指定位於應用程式中的AIR應用程式signatures.xml檔案的路徑 [!DNL META-INF] 目錄

* `signingcert` 指定用於對AIR應用程式簽名的證書

>[!NOTE]
>
>要確定iOS應用程式的發佈者ID，請使用 `-s` 選項，並指定用於簽名iOS應用程式的證書。 ***Adobe Primetime需要構建可播放訪問保護內容的iOS應用程式***。
