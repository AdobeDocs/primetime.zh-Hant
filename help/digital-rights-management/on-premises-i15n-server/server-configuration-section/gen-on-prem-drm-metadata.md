---
title: 生成本地DRM元資料
description: 生成本地DRM元資料
copied-description: true
exl-id: b42e3491-081b-45bf-bd00-8fb769a97446
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 生成本地DRM元資料{#generate-the-on-premises-drm-metadata}

A [!DNL CreateMetadata.jar] 實用程式包含在 [!DNL create_metadata] 的子菜單。 此實用程式的要點是建立本地DRM元資料，該元資料將啟動客戶端針對指定的本地個性化伺服器執行個性化進程。

1. 使用下列檔案更新Mogine DRM參考實現 — 命令行工具：

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      兩個JAR檔案可以位於 [!DNL Command Line Tools/libs] 的子菜單。 的 [!DNL createMetadata.properties] 檔案可以位於 [!DNL flashaccesstools.properties] 的子菜單。

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

包括 [!DNL examplecreate.sh] 演示元資料示例建立的指令碼。 在嘗試生成元資料之前，請確保在指令碼和屬性檔案中配置許可證伺服器URL和個性化伺服器URL。

實用程式之輸入值如下：

* `createMetadata.properties`  — 包含預設策略、證書位置和密碼等的屬性檔案。
* `indivCert`  — 包含個性化傳輸證書的PKCS12檔案
* `indivURL`  — 本地個性化伺服器的URL

輸出檔案是DRM客戶端將使用的本地DRM元資料檔案。 例如：

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.
