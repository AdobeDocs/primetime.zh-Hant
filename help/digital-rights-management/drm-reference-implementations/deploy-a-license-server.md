---
title: 部署許可證伺服器
description: 部署許可證伺服器
copied-description: true
exl-id: 1439a5b2-eccb-41b7-a4d3-0673e727fb13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 部署許可證伺服器{#deploy-the-license-server}

1. 將您的參考實現戰爭檔案複製到 `webapps` 目錄。

   要按原樣使用參考實現許可證伺服器，您只需複製許可證伺服器WAR檔案( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) `webapps` 目錄。

   如果要自定義引用實施許可證伺服器，請複製您從中構建的伺服器戰爭檔案 `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` 到 `webapps` 的子菜單。

   >[!NOTE]
   >
   >如果以前部署了許可證伺服器WAR檔案，則可能需要刪除 [!DNL webapps] Tomcat伺服器上的目錄：
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >不部署 [!DNL edsws.war] 除非您要求向後相容Flash媒體Rights Management(FMRMS)v1.5內容。 （這是非常少見的要求。）
   >
   >如果希望阻止Tomcat解包WAR檔案，請編輯 `server.xml` 的 `conf` 目錄和集 `unpackWARs` 至 `false`。

1. 複製 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` 目錄 [!DNL tomcat] 的子菜單。

   的 [!DNL resources] 目錄包括：

   * [!DNL flashaccesstools.properties]  — 許可證伺服器屬性檔案。
   * [!DNL log4j.xml]  — 許可證伺服器日誌配置
   * [!DNL *.pol] - DRM策略檔案示例。

   此外，您還可以選擇將Adobe證書檔案複製到此位置。

1. 在中修改許可證伺服器設定 [!DNL flashaccesstools.properties] 以反映伺服器設定。

   至少為以下屬性設定值：

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

1. 編輯 `catalina.properties` 檔案 `conf` 目錄；添加您的位置 [!DNL resources] 目錄（或儲存屬性檔案和其他資源檔案的備用位置） `shared.loader` 屬性。

   例如，如果 `flashaccess-refimpl.properties` 位於[!DNL中 [Tomcat首頁]\resources\]:

   ```
   shared.loader=..\resources
   ```

   這裡 `flashaccess-refimpl.properties` 類路徑中。
1. 確保您的其他資源檔案( [!DNL log4j.xml]，策略檔案，認證) [!DNL resources] 目錄，或在類路徑及其中指定的位置上 [!DNL flashaccess-refimpl.properties]。

   您可能希望初始運行 `log4j` 調試模式。 在 [!DNL log4j.xml]。 `debug` 為true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. 從Tomcat [!DNL bin] 目錄，啟動伺服器。

   在Linux上：

   ```
   catalina.sh start
   ```

   在Windows上：

   ```
   catalina.bat start
   ```
