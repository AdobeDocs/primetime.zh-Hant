---
seo-title: 概觀
title: 概觀
uuid: f45c6b58-53c5-41e0-be3d-590231dd214a
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# AIR Publisher ID公用程式 {#air-publisher-id-utility}

當您建立AIR檔案時，AIR開發人員工具(ADT)會自動產生發佈者ID。 AIR Publisher ID公用程式( [!DNL AdobePublisherIDUtility.jar])會計算AIR應用程式的Publisher ID。

發佈者ID是您用來建立AIR檔案的憑證唯一的。 如果您針對多個AIR應用程式重複使用相同的憑證，所有AIR應用程式都有相同的發佈者ID。 成功發行1.5.2的AIR版本不會將產生的發佈者ID新增至檔案。 因此，如果您打算使用AIR應用程式白名單，請使用此工具來判斷發佈者ID。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>用於AIR白名單實施的發佈者ID與應用程式發佈者在應用程式檔案中指定的發佈者ID不相 [!DNL application.xml] 同。

## AIR Publisher ID公用程式命令列用法 {#air-publisher-id-utility-command-line-usage}

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

* 
   * `signaturefile`*指定AIR應用程式檔案的路徑，位 [!DNL signatures.xml] 於應用程式目錄中 [!DNL META-INF]

* `signingcert` 指定用來簽署AIR應用程式的憑證

>[!NOTE]
>
>若要決定Android應用程式的發佈者ID，您必須使用選 `-s` 項來指定用來簽署Android應用程式套件(APK)的憑證。 Primetime DRM是建立Android應用程式的必要條件，以播放受DRM保護的內容。