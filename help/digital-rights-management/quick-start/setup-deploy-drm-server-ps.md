---
title: 針對受保護的串流設定和部署伺服器
description: 針對受保護的串流設定和部署伺服器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 設定並部署受保護串流的伺服器{#set-up-and-deploy-the-server-for-protected-streaming}

1. 在Primetime DRM DVD上設定設定資料夾：

   `\Adobe Access Server for Protected Streaming\configs\`
1. 將範例`configs`資料夾複製至`<Tomcat_installation_dir>`，並將複製的資料夾重新命名為`licenseserver`。

   配置資料夾的路徑現在應為`<Tomcat_install_dir>\licenseserver\`。
1. 運行`Scrambler.bat`以獲取Primetime DRM `<DVD>` `\Adobe Access Server for Protected Streaming\`目錄中傳輸和許可伺服器PFX檔案的加密口令：

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. 將PFX檔案複製到`<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\`目錄。
1. 在`<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`中編輯對應的租用戶設定，並進行下列設定：

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. 運行`Validator.bat`實用程式以驗證配置是否有效：

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. 將`flashaccessserver.war`檔案從光碟複製到`<TomcatInstallDir>\webapps\`目錄。
1. 如果Tomcat正在運行，請在命令窗口中按`<CTRL-C>`停止運行的Tomcat實例（如果它是從命令窗口啟動的）。 如果Tomcat是作為Windows服務安裝的，您也可以從Windows服務應用程式中停止伺服器。
1. 要啟動Tomcat，請輸入以下命令：

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. 若要驗證設定，請在瀏覽器中輸入下列URL:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
