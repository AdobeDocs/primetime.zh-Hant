---
description: 'null'
seo-description: 'null'
seo-title: 部署授權伺服器
title: 部署授權伺服器
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 29149594c4b41956a091ef27093304e74ff15f2f

---


# 部署授權伺服器{#deploy-the-license-server}

1. 將您的參考實施war檔案複製到Tomcat `webapps` 伺服器上的目錄。

   要按原樣使用參考實施許可證伺服器，您只需將許可證伺服器WAR檔案( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`)複製到Tomcat服 `webapps` 務器上的目錄。

   如果要自定義參考實施許可證伺服器，請將從中構建的伺服器war檔案複製 `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` 到目 `webapps` 錄。

   >[!NOTE]
   >
   >如果先前已部署許可證伺服器WAR檔案，則可能需要刪除Tomcat伺服器目錄中 [!DNL webapps] 未打包的WAR目錄：       >
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >除非您 [!DNL edsws.war] 需要向後與Flash Media Rights Management(FMRMS)v1.5內容相容，否則不要部署。 （這是非常罕見的要求。）
   >
   >如果希望防止Tomcat解壓縮WAR檔案，請在目 `server.xml` 錄中 `conf` 編輯並設定 `unpackWARs` 為 `false`。

1. 將目錄的整個內 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` 容複製到 [!DNL tomcat] 目錄。

   目 [!DNL resources] 錄包括：

   * [!DNL flashaccesstools.properties] -許可證伺服器屬性檔案。
   * [!DNL log4j.xml] -許可證伺服器日誌配置
   * [!DNL *.pol] - DRM策略檔案示例。
   此外，您也可以選擇將Adobe認證檔案複製到此位置。

1. 在中修改許可證伺服器設 [!DNL flashaccesstools.properties] 置，以反映伺服器設定。

   至少要為下列屬性設定值：

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

1. 編輯Tomcat `catalina.properties` 目錄中的 `conf` 檔案；將目錄的位 [!DNL resources] 置（或儲存屬性檔案和其他資源檔案的備用位置）添加到屬 `shared.loader` 性。

   例如，如果您位 `flashaccess-refimpl.properties` 於[!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   這會將其 `flashaccess-refimpl.properties` 放在類路徑中。
1. 確保您的其他資源檔案( [!DNL log4j.xml]、策略檔案、認證)位於目錄中，或 [!DNL resources] 者位於類路徑及其中指定的位置上 [!DNL flashaccess-refimpl.properties]。

   您可能會想在除錯模式 `log4j` 下開始執行。 在 [!DNL log4j.xml]中， `debug` 設定為true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. 從Tomcat目 [!DNL bin] 錄啟動伺服器。

   在Linux上：

   ```
   catalina.sh start
   ```

   在Windows上：

   ```
   catalina.bat start
   ```
