---
seo-title: 生成內部DRM元資料
title: 生成內部DRM元資料
uuid: 89d53924-1a8d-42d4-a716-ce4f4566b6bf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 生成內部DRM元資料{#generate-the-on-premises-drm-metadata}

檔案 [!DNL CreateMetadata.jar] 夾中包含一個實用 [!DNL create_metadata] 程式。 該實用程式的要點是建立內部DRM元資料，該元資料將啟動客戶機對指定的內部個性化伺服器執行個性化處理。

1. 使用下列檔案更新Primetime DRM參考實施——命令行工具：

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      兩個JAR檔案可以駐留在資料夾中 [!DNL Command Line Tools/libs] 。 檔案 [!DNL createMetadata.properties] 可以駐留在檔案旁 [!DNL flashaccesstools.properties] 邊。

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

內含的指 [!DNL examplecreate.sh] 令碼會示範中繼資料的範例建立。 嘗試產生中繼資料之前，請務必先在指令碼和屬性檔案中設定授權伺服器URL和個人化伺服器URL。

該公用程式的輸入如下：

* `createMetadata.properties` -包含預設策略、證書位置和密碼等的屬性檔案。
* `indivCert` -包含個性化傳輸證書的PKCS12檔案
* `indivURL` -內部個人化伺服器的URL

輸出檔案是將由DRM客戶機使用的內部DRM元資料檔案。 例如：

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.