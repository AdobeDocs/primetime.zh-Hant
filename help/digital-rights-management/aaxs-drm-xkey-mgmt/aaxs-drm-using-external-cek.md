---
description: 使用外部CEK功能，使用您現有的CKMS來開發和封裝授權。
seo-description: 使用外部CEK功能，使用您現有的CKMS來開發和封裝授權。
seo-title: 使用外部CEK購買及封裝授權
title: 使用外部CEK購買及封裝授權
uuid: 1bfd8c6c-4ae9-47de-8247-085b5360127d
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0

---


# 使用外部CEK購買及封裝授權{#using-external-cek-to-vend-and-package-licenses}

使用外部CEK功能，使用您現有的CKMS來開發和封裝授權。

## EncryptContentWithExternalKey.java

這是一種命令列工具，可讓AAXS加密視訊並建立不包含 *CEK* （受AAXS授權伺服器公用憑證保護）的中繼資料。 工具會將CEK ID內嵌在視訊的中繼資料中。

在取得授權期間，AAXS授權伺服器會在中繼資料中觀察標幟，指出此內容是使用外部CEK加以保護的。 授權伺服器會從中繼資料擷取CEK ID，然後查詢安全儲存庫/CKMS以擷取適當的CEK。

## 封裝工作流程

1. 請確定您使用的是Java 1.6.0_24或更新版本。
1. 若要查看工具使用情形： `java -jar AdobePackager_ExternalCEK.jar`
1. 若要封裝內容：

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* Java原始碼可以使用包含的ANT來構建 `build-samples.xml`
>* Flash Access SDK( `adobe-flashaccess-sdk.jar`)必須位於類路徑中
>



## 伺服器工作流程

1. 設定參考實作。
1. 如果存在，請清除先前的「參考實施」部署：

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. 確認您的 [!DNL CEKDepot.properties][!DNL flashaccess-refimpl.properties]

1. 從Adobe Primetime Player開始申請授權
1. 觀察參照實施日誌中類似以下內容：

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. 您可能必須變更設 [!DNL log4j.xml] 定，才能在某 `DEBUG` 個層級 `INFO` 登入（預設設定）

## 已知問題

無
