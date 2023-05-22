---
title: 包加密內容
description: 包加密內容
copied-description: true
exl-id: e5792917-8172-48b0-8792-7a7e942596c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 包加密內容{#package-encrypted-content}

1. 複製 `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` 本地檔案系統的目錄。
1. 在您的本地 `Command Line Tools\` 資料夾，更新 `flashaccesstools.properties` 檔案以與伺服器一起使用。

   必須至少修改以下屬性：

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`:許可證伺服器證書的路徑(通常以 [!DNL .cer]。 [!DNL .der] 或 [!DNL .pem])。

   * `encrypt.license.serverurl=[license-server-url]`:您的許可證伺服器URL，例如：    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`。

   * `encrypt.license.servercert=[transport-certificate.cer]`:傳輸證書的路徑(通常以 [!DNL .cer]。 [!DNL .der]或 [!DNL .pem])。

   * `encrypt.sign.certfile=[packager-credentials.pfx]`:包裝程式證書的路徑(以 [!DNL .pfx])。

   * `encrypt.sign.certpass=[password]`:Packager證書的密碼。
   >[!NOTE]
   >
   >確保不要對密碼進行加擾。

1. 建立策略。

   在您的本地 `Command Line Tools\` 資料夾，運行以下命令：

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   此命令建立名為 [!DNL examplepolicy.pol] 使用匿名許可證伺服器身份驗證( `-x` 選項。
1. 將要加密的MP4、FLV或F4V視頻檔案複製到本地 `Command Line Tools\` 的子菜單。
1. 打包您的內容。

   假設源視頻檔案 [!DNL sample.mp4]。 在您的本地 `Command Line Tools\` 資料夾，運行以下命令：

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >如果要打包HLS、HDS或DASH內容，必須使用其他打包工具，如 [Adobe Primetime離線打包器](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)。

1. 複製加密的檔案對象（在本例中） [!DNL sample_encrypted.mp4] 和 [!DNL sample_encrypted.mp4.metadata]) `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`。

此時，您已完成流程的打包階段。

>[!NOTE]
>
>有關用於打包內容、建立策略等的命令行工具的詳細資訊，請參見 [Adobe PrimetimeDRM命令行工具](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md)。
