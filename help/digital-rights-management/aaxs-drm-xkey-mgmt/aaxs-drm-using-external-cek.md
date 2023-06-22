---
description: 使用「外部CEK」功能，以使用現有CKMS來銷售及封裝授權。
title: 使用外部CEK來銷售和封裝授權
exl-id: 3944624a-099e-4fc0-b829-6ab154a53758
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 使用外部CEK來銷售和封裝授權{#using-external-cek-to-vend-and-package-licenses}

使用「外部CEK」功能，以使用現有CKMS來銷售及封裝授權。

## EncryptContentWithExternalKey.java

這是命令列工具，可對AAXS加密視訊並建立中繼資料，將 *not* 包含CEK （受AAXS授權伺服器的公開憑證保護）。 反之，此工具會將CEK ID內嵌至視訊的中繼資料中。

在取得授權期間，AAXS授權伺服器會觀察中繼資料中的旗標，指出此內容已使用外部CEK受到保護。 授權伺服器將從中繼資料中擷取CEK ID，然後查詢安全存放庫/CKMS以擷取適當的CEK。

## 封裝工作流程

1. 確保您使用的是Java 1.6.0_24或更新版本。
1. 若要檢視工具使用情形： `java -jar AdobePackager_ExternalCEK.jar`
1. 若要封裝內容：

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* 可以使用隨附的ANT建置Java原始程式碼 `build-samples.xml`
>* FLASH ACCESSSDK ( `adobe-flashaccess-sdk.jar`)必須在類別路徑上
>


## 伺服器工作流程

1. 設定參考實作。
1. 如果有的話，請清理先前的參考實作部署：

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. 確認存在 [!DNL CEKDepot.properties] 檔案與您的 [!DNL flashaccess-refimpl.properties]

1. 從Adobe Primetime Player起始授權請求
1. 觀察參考實作記錄，以瞭解類似下列的內容：

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. 您可能必須變更您的 [!DNL log4j.xml] 記錄位置的設定 `DEBUG` level ( `INFO` 已預設設定)

## 已知問題

無
