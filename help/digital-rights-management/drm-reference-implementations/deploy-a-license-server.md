---
title: 部署授權伺服器
description: 部署授權伺服器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 部署許可證伺服器{#deploy-the-license-server}

1. 將您的參考實作war檔案複製到Tomcat伺服器上的`webapps`目錄。

   要按原樣使用參考實施許可證伺服器，您只需將許可證伺服器WAR檔案(`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`)複製到Tomcat伺服器上的`webapps`目錄。

   如果要自定義參考實施許可證伺服器，請將從`DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars`構建的伺服器war檔案複製到`webapps`目錄。

   >[!NOTE]
   >
   >如果先前已部署許可證伺服器WAR檔案，則可能需要刪除Tomcat伺服器[!DNL webapps]目錄中未打包的WAR目錄：
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >除非您需要向後相容Flash媒體Rights Management(FMRMS)v1.5內容，否則不要部署[!DNL edsws.war]。 （這是非常罕見的要求。）
   >
   >如果希望防止Tomcat解壓縮WAR檔案，請編輯`conf`目錄中的`server.xml`，並將`unpackWARs`設定為`false`。

1. 將`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\`目錄的整個內容複製到[!DNL tomcat]目錄中。

   [!DNL resources]目錄包括：

   * [!DNL flashaccesstools.properties] -許可證伺服器屬性檔案。
   * [!DNL log4j.xml] -許可證伺服器日誌配置
   * [!DNL *.pol] - DRM策略檔案示例。

   此外，您也可以選擇將Adobe認證檔案複製到此位置。

1. 修改[!DNL flashaccesstools.properties]中的許可證伺服器設定以反映伺服器設定。

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

1. 編輯Tomcat `conf`目錄中的`catalina.properties`檔案；將[!DNL resources]目錄的位置（或儲存屬性檔案和其他資源檔案的備用位置）添加到`shared.loader`屬性。

   例如，如果`flashaccess-refimpl.properties`位於[!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   這會將`flashaccess-refimpl.properties`放在類路徑上。
1. 請確定您的其他資源檔案（[!DNL log4j.xml]、策略檔案、認證）位於[!DNL resources]目錄中，或者位於類路徑及其在[!DNL flashaccess-refimpl.properties]中指定的位置上。

   您可能想在除錯模式下開始執行`log4j`。 在[!DNL log4j.xml]中，將`debug`設為true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. 從Tomcat [!DNL bin]目錄啟動伺服器。

   在Linux上：

   ```
   catalina.sh start
   ```

   在Windows上：

   ```
   catalina.bat start
   ```
