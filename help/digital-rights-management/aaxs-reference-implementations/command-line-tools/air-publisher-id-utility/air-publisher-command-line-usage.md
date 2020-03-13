---
seo-title: 命令列使用
title: 命令列使用
uuid: 54b1e867-c6cc-4355-b8e6-a7ec910bd33d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 命令列使用 {#command-line-usage}

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

* 
   * `signaturefile`*指定AIR應用程式signatures.xml檔案的路徑，位於應用程式目 [!DNL META-INF] 錄

* `signingcert` 指定用於簽署AIR應用程式的憑證

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>若要決定iOS應用程式的發佈者ID，請使用 `-s` 選項並指定用來簽署iOS應用程式的憑證。 ***Adobe Primetime是建立可播放受存取保護內容的iOS應用程式的必要工具***。

