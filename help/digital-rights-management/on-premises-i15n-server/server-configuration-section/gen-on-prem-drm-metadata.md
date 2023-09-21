---
title: 產生內部部署DRM中繼資料
description: 產生內部部署DRM中繼資料
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 產生內部部署DRM中繼資料{#generate-the-on-premises-drm-metadata}

A [!DNL CreateMetadata.jar] 公用程式包含在 [!DNL create_metadata] 資料夾。 此公用程式的目的是建立On Premises DRM中繼資料，此中繼資料將啟動使用者端對指定的On Premises Individualization Server執行個人化程式。

1. 使用下列檔案更新Primetime DRM參照實作 — 命令列工具：

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

     兩個JAR檔案可以位於 [!DNL Command Line Tools/libs] 資料夾。 此 [!DNL createMetadata.properties] 檔案可位於旁邊 [!DNL flashaccesstools.properties] 檔案。

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

包含一個 [!DNL examplecreate.sh] 示範中繼資料範例建立的指令碼。 嘗試產生中繼資料之前，請務必在指令碼和屬性檔案中設定授權伺服器URL和個人化伺服器URL。

公用程式的輸入如下：

* `createMetadata.properties`  — 包含預設原則、憑證位置和密碼等的屬性檔案。
* `indivCert`  — 包含個人化傳輸憑證的PKCS12檔案
* `indivURL`  — 內部部署個人化伺服器的URL

輸出檔案是DRM使用者端使用的內部部署DRM中繼資料檔案。 例如：

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.
