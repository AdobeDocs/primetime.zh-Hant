---
seo-title: 針對受保護的串流設定和部署伺服器
title: 針對受保護的串流設定和部署伺服器
uuid: 300a1b63-0bf0-48a8-977d-212563025c19
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 針對受保護的串流設定和部署伺服器 {#set-up-and-deploy-the-server-for-protected-streaming}

1. 在Primetime DRM DVD上設定設定資料夾：

   `\Adobe Access Server for Protected Streaming\configs\`
1. 將範例資料 `configs` 夾複製到 `<Tomcat_installation_dir>` 您的檔案夾，並將複製的檔案夾重新命名為 `licenseserver`。

   配置資料夾的路徑現在應為 `<Tomcat_install_dir>\licenseserver\`。
1. 運 `Scrambler.bat` 行以獲取Primetime DRM目錄中傳輸和許可伺服器PFX檔案的加密 `<DVD>` 密 `\Adobe Access Server for Protected Streaming\` 碼：

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. 將PFX檔案複製到目 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` 錄。
1. 使用下列設定，在中編 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`輯對應的租用戶設定：

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. 運行該實 `Validator.bat` 用程式以驗證配置是否有效：

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. 將文 `flashaccessserver.war` 件從CD複製到目 `<TomcatInstallDir>\webapps\` 錄。
1. 如果Tomcat正在運行，請在命令窗口中按 `<CTRL-C>` 下（如果是從命令窗口啟動）以停止運行的Tomcat實例。 如果Tomcat是作為Windows服務安裝的，您也可以從Windows服務應用程式中停止伺服器。
1. 要啟動Tomcat，請輸入以下命令：

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. 若要驗證設定，請在瀏覽器中輸入下列URL:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
