---
description: 使用外部CEK功能使用現有CKMS進行許可和包裝。
title: 使用外部CEK獲取許可證和包許可證
exl-id: 3944624a-099e-4fc0-b829-6ab154a53758
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 使用外部CEK獲取許可證和包許可證{#using-external-cek-to-vend-and-package-licenses}

使用外部CEK功能使用現有CKMS進行許可和包裝。

## EncryptContentWithExternalKey.java

這是一個命令行工具，它將AAXS加密視頻並建立元資料 *不* 包含CEK（使用AAXS許可證伺服器的公共證書進行保護）。 相反，該工具將CEK ID嵌入到視頻的元資料中。

在獲取許可證期間，AAXS許可證伺服器觀察元資料中的標誌，該標誌標識此內容是使用外部CEK進行保護的。 許可證伺服器將從元資料中提取CEK ID，然後查詢安全儲存庫/CKMS以檢索相應的CEK。

## 打包工作流

1. 確保使用的是Java 1.6.0_24或更高版本。
1. 要查看工具用法： `java -jar AdobePackager_ExternalCEK.jar`
1. 要打包內容：

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* 可以使用包含的ANT生成Java原始碼 `build-samples.xml`
>* Flash AccessSDK( `adobe-flashaccess-sdk.jar`)必須位於類路徑上
>


## 伺服器工作流

1. 設定「參考實施」。
1. 如果存在，請清除以前的「參考實施」部署：

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. 驗證是否存在 [!DNL CEKDepot.properties] 檔案 [!DNL flashaccess-refimpl.properties]

1. 從Adobe Primetime播放器啟動許可請求
1. 觀察Ref Impl日誌中類似以下內容：

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. 你可能必須改變 [!DNL log4j.xml] 登錄設定 `DEBUG` 級別( `INFO` 預設設定)

## 已知問題

無
