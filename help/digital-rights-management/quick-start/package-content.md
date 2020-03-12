---
seo-title: 封裝加密內容
title: 封裝加密內容
uuid: 1e271167-107d-41df-8a7c-3075cb3acc0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 封裝加密內容{#package-encrypted-content}

1. 將目錄復 `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` 制到本地檔案系統。
1. 在本機資 `Command Line Tools\` 料夾中，更新檔 `flashaccesstools.properties` 案以搭配您的伺服器運作。

   您至少必須修改下列屬性：

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`:您的「授權伺服器憑證」的路徑(通常以 [!DNL .cer]、 [!DNL .der] 或 [!DNL .pem]結尾)。

   * `encrypt.license.serverurl=[license-server-url]`:您的授權伺服器URL，例如：   `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`。

   * `encrypt.license.servercert=[transport-certificate.cer]`:傳輸憑證的路徑(通常以、 [!DNL .cer]或 [!DNL .der]結尾 [!DNL .pem])。

   * `encrypt.sign.certfile=[packager-credentials.pfx]`:Packager憑證的路徑(以 [!DNL .pfx]結尾)。

   * `encrypt.sign.certpass=[password]`:Packager憑證的密碼。
   >[!NOTE]
   >
   >請確定您不要亂碼。

1. 建立原則。

   在本機資 `Command Line Tools\` 料夾中，執行下列命令：

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   此命令將建立一個名為的策略文 [!DNL examplepolicy.pol] 件，該檔案使用匿名許可證伺服器驗證( `-x` 選項)。
1. 將您要加密的MP4、FLV或F4V視訊檔案複製至本機資 `Command Line Tools\` 料夾。
1. 封裝您的內容。

   假設您的來源視訊檔案是 [!DNL sample.mp4]。 在本機資 `Command Line Tools\` 料夾中，執行下列命令：

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >如果您想要封裝HLS、HDS或DASH內容，則必須使用不同的封裝工具，例如 [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)。

1. 將加密的檔案對象(在本例中為 [!DNL sample_encrypted.mp4] 和 [!DNL sample_encrypted.mp4.metadata])複製到 `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`。

此時，您已完成此程式的封裝階段。

>[!NOTE]
>
>如需封裝內容、建立原則等命令列工具的詳細資訊，請參閱 [Adobe Primetime DRM命令列工具](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md)。
