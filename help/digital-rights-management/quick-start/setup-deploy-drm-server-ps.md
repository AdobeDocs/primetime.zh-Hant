---
title: 設定和部署受保護流的伺服器
description: 設定和部署受保護流的伺服器
copied-description: true
exl-id: de1488e6-ccee-49e6-999e-6c6762dd55be
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 設定和部署受保護流的伺服器 {#set-up-and-deploy-the-server-for-protected-streaming}

1. 在Gimfire DRM DVD上設定配置資料夾：

   `\Adobe Access Server for Protected Streaming\configs\`
1. 複製示例 `configs` 資料夾 `<Tomcat_installation_dir>` 並將複製的資料夾更名為 `licenseserver`。

   配置資料夾的路徑現在應為 `<Tomcat_install_dir>\licenseserver\`。
1. 運行 `Scrambler.bat` 獲取黃金時段DRM中傳輸和許可伺服器PFX檔案的加密密碼 `<DVD>` `\Adobe Access Server for Protected Streaming\` 目錄：

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. 將PFX檔案複製到 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` 的子菜單。
1. 在中編輯相應的租戶配置 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`，具有以下設定：

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. 運行 `Validator.bat` 用於驗證配置有效的實用程式：

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. 複製 `flashaccessserver.war` 從CD到 `<TomcatInstallDir>\webapps\` 的子菜單。
1. 如果Tomcat正在運行，請按 `<CTRL-C>` 命令窗口中（如果是從命令窗口啟動）。 如果Tomcat作為Windows服務安裝，也可以從Windows服務應用程式中停止伺服器。
1. 要啟動Tomcat，請輸入以下命令：

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. 要驗證設定，請在瀏覽器中輸入以下URL:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
