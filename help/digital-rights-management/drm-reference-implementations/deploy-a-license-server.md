---
title: 部署授權伺服器
description: 部署授權伺服器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 部署授權伺服器{#deploy-the-license-server}

1. 將您的參考實作war檔案複製到 `webapps` 目錄。

   若要照原樣使用參照實作許可證伺服器，您只需複製許可證伺服器WAR檔案( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`)到 `webapps` 目錄。

   如果您要自訂參照實作許可證伺服器，請複製您從中建立的伺服器war檔案 `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` 至 `webapps` 目錄。

   >[!NOTE]
   >
   >如果您先前已部署許可證伺服器WAR檔案，您可能需要刪除 [!DNL webapps] Tomcat伺服器上的目錄：
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]

   >[!NOTE]
   >
   >不要部署 [!DNL edsws.war] 除非您需要回溯相容於Flash MediaRights Management(FMRMS) v1.5內容。 （這是非常罕見的要求。）
   >
   >如果您不想讓Tomcat解壓縮WAR檔案，請編輯 `server.xml` 在 `conf` 目錄和集合 `unpackWARs` 至 `false`.

1. 複製 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` 目錄至您的 [!DNL tomcat] 目錄。

   此 [!DNL resources] 目錄包含：

   * [!DNL flashaccesstools.properties]  — 許可證伺服器屬性檔案。
   * [!DNL log4j.xml]  — 授權伺服器記錄設定
   * [!DNL *.pol] - DRM原則檔範例。

   此外，您也可以選擇將Adobe認證檔案複製到此位置。

1. 修改中的授權伺服器設定 [!DNL flashaccesstools.properties] 以反映您的伺服器設定。

   請至少設定下列屬性的值：

   * `config.resourcesDirectory`
   * `HandlerConfiguration.ServerTransportCredential`
   * `HandlerConfiguration.ServerTransportCredential.password`
   * `LicenseHandler.ServerCredential`
   * `LicenseHandler.ServerCredential.password`
   * `MetaDataConverter.SignatureParameters.ServerCredential`
   * `MetaDataConverter.SignatureParameters.ServerCredential.password`
   * `V2KeyParameters.LicenseServerUrl`
   * `V2KeyParameters.KeyOptions.AsymmetricKeyOptions.Certificate`
   * V2KeyParameters.LicenseServerTransportCertificate

1. 編輯 `catalina.properties` Tomcat中的檔案 `conf` 目錄；新增您的位置 [!DNL resources] 目錄（或您儲存屬性檔案和其他資源檔案的替代位置）至 `shared.loader` 屬性。

   例如，如果您擁有 `flashaccess-refimpl.properties` 位於[！DNL [Tomcat首頁]\resources\]：

   ```
   shared.loader=..\resources
   ```

   此地標 `flashaccess-refimpl.properties` 在類別路徑上。
1. 確定您的其他資源檔案( [!DNL log4j.xml]，原則檔、認證)位於 [!DNL resources] 目錄，或位於類別路徑上，以及它們在 [!DNL flashaccess-refimpl.properties].

   您一開始可能會想要執行 `log4j` 在偵錯模式中。 在 [!DNL log4j.xml]，設定 `debug` 為true：

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. 從Tomcat [!DNL bin] 目錄，啟動您的伺服器。

   在Linux上：

   ```
   catalina.sh start
   ```

   在Windows上：

   ```
   catalina.bat start
   ```
