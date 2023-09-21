---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# AIR發佈者ID公用程式 {#air-publisher-id-utility}

建置AIR檔案時，AIR Developer Tool (ADT)會自動產生發佈者ID。 AIR發佈者ID公用程式( [!DNL AdobePublisherIDUtility.jar])計算AIR應用程式的發佈者ID。

發行者ID是您用來建置AIR檔案之憑證的唯一一個。 如果您在多個AIR應用程式中重複使用相同的憑證，則所有AIR應用程式都會使用相同的發行者ID。 成功發行版本1.5.2的AIR不會將產生的發行者ID新增至檔案。 因此，如果您打算使用AIR應用程式允許清單，請使用此工具來決定發佈者ID。

>[!NOTE]
>
>用於AIR允許清單強制的發佈者ID與應用程式發佈者在應用程式中指定的發佈者ID不同 [!DNL application.xml] 檔案。

## AIR發佈者ID公用程式命令列用法 {#air-publisher-id-utility-command-line-usage}

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
>若要判斷Android應用程式的發佈者ID，您需要使用 `-s` 用於指定用於簽署Android應用程式套件(APK)的憑證的選項。 建立可以播放Primetime DRM保護內容的Android應用程式需要Primetime DRM。
