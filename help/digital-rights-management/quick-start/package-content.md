---
title: 封裝加密的內容
description: 封裝加密的內容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 封裝加密的內容{#package-encrypted-content}

1. 複製 `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` 目錄至您的本機檔案系統。
1. 在您的本機 `Command Line Tools\` 資料夾，更新 `flashaccesstools.properties` 使用伺服器的檔案。

   您至少必須修改下列屬性：

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`：您的License Server憑證的路徑(通常結尾為 [!DNL .cer]， [!DNL .der] 或 [!DNL .pem])。

   * `encrypt.license.serverurl=[license-server-url]`：您的授權伺服器URL，例如：    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`：傳輸憑證的路徑(通常結尾為 [!DNL .cer]， [!DNL .der]，或 [!DNL .pem])。

   * `encrypt.sign.certfile=[packager-credentials.pfx]`：您的Packager憑證的路徑(結尾為 [!DNL .pfx])。

   * `encrypt.sign.certpass=[password]`：您的Packager憑證密碼。

   >[!NOTE]
   >
   >請確定您未加擾密碼。

1. 建立原則。

   在您的本機 `Command Line Tools\` 資料夾，執行以下命令：

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   這個命令會建立一個名為的原則檔 [!DNL examplepolicy.pol] 使用匿名授權伺服器驗證(此類 `-x` 選項)。
1. 將您要加密的MP4、FLV或F4V視訊檔案複製到本機 `Command Line Tools\` 資料夾。
1. 封裝您的內容。

   假設您的來源視訊檔案為 [!DNL sample.mp4]. 在您的本機 `Command Line Tools\` 資料夾，執行以下命令：

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >如果要封裝HLS、HDS或DASH內容，必須使用不同的封裝工具，例如 [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. 複製加密的檔案成品（在此案例中） [!DNL sample_encrypted.mp4] 和 [!DNL sample_encrypted.mp4.metadata])至 `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

此時，您已完成流程的封裝階段。

>[!NOTE]
>
>如需封裝內容、建立原則等之命令列工具的詳細資訊，請參閱 [Adobe Primetime DRM命令列工具](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
