---
title: 概觀
description: 概觀
copied-description: true
exl-id: 07f2ef0b-c6aa-4574-a3ae-18685a090cf2
source-git-commit: a1fc67b708f3d5821532d3827639adbadf15f6b4
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# AIR Publisher ID公用程式 {#air-publisher-id-utility}

當您建立AIR檔案時，AIR Developer Tool (ADT)會自動產生發佈者ID。 AIR Publisher ID公用程式( [!DNL AdobePublisherIDUtility.jar])計算AIR應用程式的發行者ID。

發行者ID是您用來建立AIR檔案的憑證所獨有的。 如果您在多個AIR應用程式中重複使用相同的憑證，則所有AIR應用程式都會使用相同的發行者ID。 成功發行版本1.5.2的AIR發行版本不會將產生的發行者ID新增至檔案。 因此，如果您打算使用AIR應用程式允許清單，請使用此工具來決定發行者ID。

>[!NOTE]
>
>用於AIR允許清單強制執行的發行者ID與應用程式發行者在應用程式中指定的發行者ID不同 [!DNL application.xml] 檔案。

## AIR Publisher ID公用程式命令列使用方式 {#air-publisher-id-utility-command-line-usage}

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

* `signaturefile` 指定AIR應用程式的路徑 [!DNL signatures.xml] 檔案，位於應用程式中 [!DNL META-INF] 目錄

* `signingcert` 指定用於簽署AIR應用程式的憑證

>[!NOTE]
>
>若要判斷Android應用程式的發行者ID，您需要使用 `-s` 選項來指定用於簽署Android應用程式套件(APK)的憑證。 建立可以播放受Primetime DRM保護內容的Android應用程式需要Primetime DRM。
