---
title: 概述
description: 概述
copied-description: true
exl-id: 07f2ef0b-c6aa-4574-a3ae-18685a090cf2
source-git-commit: a1fc67b708f3d5821532d3827639adbadf15f6b4
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# AIR發佈者ID實用程式 {#air-publisher-id-utility}

生成AIR檔案時，AIR開發工具(ADT)會自動生成發佈者ID。 AIR發佈者ID實用程式( [!DNL AdobePublisherIDUtility.jar])計算AIR應用程式的發佈者ID。

發佈者ID對於用於生成AIR檔案的證書是唯一的。 如果對多個AIR應用程式重複使用相同的證書，則所有AIR應用程式都具有相同的發佈者ID。 成功於1.5.2版的AIR發行版不會將生成的發佈者ID添加到檔案中。 因此，如果您計畫使用AIR應用程式允許清單，請使用此工具確定發佈者ID。

>[!NOTE]
>
>用於AIR允許清單強制的發佈者ID與應用程式發佈者在應用程式中指定的發佈者ID不同 [!DNL application.xml] 的子菜單。

## AIR發佈者ID實用程式命令行用法 {#air-publisher-id-utility-command-line-usage}

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

* `signaturefile` 指定到AIR應用程式的路徑 [!DNL signatures.xml] 檔案，位於應用程式中 [!DNL META-INF] 目錄

* `signingcert` 指定用於對AIR應用程式簽名的證書

>[!NOTE]
>
>要確定Android應用程式的發佈者ID，您需要使用 `-s` 選項，指定用於簽名Android應用程式套件(APK)的證書。 黃金時段DRM需要構建可播放黃金時段DRM保護內容的Android應用程式。
