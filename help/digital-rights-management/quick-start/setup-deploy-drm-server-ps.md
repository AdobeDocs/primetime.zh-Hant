---
title: 設定並部署伺服器以進行Protected Streaming
description: 設定並部署伺服器以進行Protected Streaming
copied-description: true
exl-id: de1488e6-ccee-49e6-999e-6c6762dd55be
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 設定並部署伺服器以進行Protected Streaming {#set-up-and-deploy-the-server-for-protected-streaming}

1. 在Primetime DRM DVD上設定設定資料夾：

   `\Adobe Access Server for Protected Streaming\configs\`
1. 複製範例 `configs` 資料夾至您的 `<Tomcat_installation_dir>` 並將複製的資料夾重新命名為 `licenseserver`.

   設定資料夾的路徑現在應為 `<Tomcat_install_dir>\licenseserver\`.
1. 執行 `Scrambler.bat` 在Primetime DRM中取得傳輸與授權伺服器PFX檔案的加密密碼 `<DVD>` `\Adobe Access Server for Protected Streaming\` 目錄：

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. 將PFX檔案複製到 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` 目錄。
1. 在中編輯對應的租使用者設定 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`，並提供下列設定：

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. 執行 `Validator.bat` 驗證組態有效性的公用程式：

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. 複製 `flashaccessserver.war` 從CD到 `<TomcatInstallDir>\webapps\` 目錄。
1. 如果Tomcat正在執行，請按一下以停止正在執行的Tomcat執行個體 `<CTRL-C>` （如果是從命令視窗啟動）。 如果Tomcat安裝為Windows服務，您也可以從Windows服務應用程式停止伺服器。
1. 若要啟動Tomcat，請輸入以下命令：

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. 若要驗證設定，請在瀏覽器中輸入下列URL：

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
