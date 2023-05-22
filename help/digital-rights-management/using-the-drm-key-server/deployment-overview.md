---
title: 部署Mogife DRM密鑰伺服器概述
description: 部署Mogife DRM密鑰伺服器概述
copied-description: true
exl-id: d70e8315-ed35-4159-842b-5066a2b1c4f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# 部署Mogife DRM密鑰伺服器 {#deploy-the-primetime-drm-key-server}

在部署Mogfire DRM密鑰伺服器之前，請確保已安裝了所需的Java和Tomcat版本。 看， [DRM密鑰伺服器要求](../../digital-rights-management/using-the-drm-key-server/requirements.md)。

黃金時段DRM密鑰伺服器下載包括 [!DNL faxsks.war]。 要部署此WAR檔案，請將該檔案複製到Tomcat的 [!DNL webapps] 的子菜單。 如果您以前部署過WAR檔案，則可能需要手動刪除解壓縮的WAR目錄， [!DNL faxsks] 在Tomcat中 [!DNL webapps] )。 要防止Tomcat解包WAR檔案，請編輯 [!DNL server.xml] Tomcat中的檔案 [!DNL conf] 目錄和設定 `unpackWARs` 屬性 `false`。

黃金時段DRM密鑰伺服器可選地使用平台特定庫(`jsafe.dll` 在Windows或 `libjsafe.so` 在Linux上)，以提高效能。 從中複製適合您的平台的庫 `thirdparty/cryptoj/platform` 到由 `PATH` 環境變數 `LD_LIBRARY_PATH` 在Linux上)。

>[!NOTE]
>
>64位版本 [!DNL jsafe] 僅當作業系統和JDK都支援64位時才應使用庫，否則請使用32位版本。

## SSL配置 {#ssl-configuration}

遠程HTTPS密鑰傳遞需要SSL。 SSL連接可以由應用程式伺服器處理（即，通過在Tomcat中配置SSL），也可以在另一個伺服器（即負載平衡器、SSL加速器或Apache）上處理。 遠程HTTPS密鑰傳遞需要SSL連接。 伺服器需要由受信任的CA頒發的SSL證書。

配置SSL有多種選項。 以下是在Apache和Tomcat中使用客戶端身份驗證配置SSL的示例。

以下示例顯示了Apache SSL配置：

```
SSLEngineon 
SSLCertificateFile "certs/server_cert.pem" 
SSLCertificateKeyFile "certs/server_key.pem" 
SSLOptions +StdEnvVars +FakeBasicAuth -ExportCertData +StrictRequire 
SSLRequireSSL 
ProxyRequests Off 
ProxyPass /https://keyserver-name:port/ 
ProxyPassReverse /https://keyserver-name:port/
```

以下示例顯示了Tomcat SSL配置。 要生成證書和密鑰檔案：

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

當提示輸入公用名稱時，請使用伺服器的完全限定域名(FQDN)。

複製 [!DNL server.cer], [!DNL server.key] 到Tomcat目錄。 在中指定以下連接器 [!DNL conf/server.xml]:

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Java系統屬性 {#java-system-properties}

您可以選擇設定以下兩個Java系統屬性來修改黃金時段DRM密鑰伺服器的配置和日誌檔案的位置：

* `KeyServer.ConfigRoot`  — 此目錄包含黃金時段DRM密鑰伺服器的所有配置檔案。 有關這些檔案內容的詳細資訊，請參見 [密鑰伺服器配置檔案](#key-server-configuration-files)。 如果未設定，則預設值為 [!DNL CATALINA_BASE/keyserver]。

* `KeyServer.LogRoot`  — 此日誌目錄包含iOS密鑰伺服器應用程式日誌。 如果未設定，則預設值與 `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot`  — 這是一個包含Xbox密鑰伺服器應用程式日誌的日誌目錄。 如果未設定，則預設值與 `KeyServer.ConfigRoot`。

如果您使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 要啟動Tomcat，可以使用 `JAVA_OPTS` 環境變數。 啟動Tomcat時，將使用此處設定的任何Java選項。 例如，設定：

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## 黃金時段DRM憑據 {#primetime-drm-credentials}

要處理來自黃金時段DRMiOS和Xbox 360客戶端的密鑰請求，必須使用由Adobe頒發的一組憑據配置黃金時段DRM密鑰伺服器。 這些憑據可以儲存在PKCS#12中( [!DNL .pfx])檔案或HSM上。

的 [!DNL .pfx] 檔案可以位於任何位置，但為便於配置，Adobe建議將 [!DNL .pfx] 檔案。 有關詳細資訊，請參見 [密鑰伺服器配置檔案](#key-server-configuration-files)。

### HSM配置 {#section_13A19E3E32934C5FA00AEF621F369877}

如果您選擇使用HSM儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立 *pkcs11.cfg* 配置檔案。 此檔案必須位於 *KeyServer.ConfigRoot* 的子菜單。 查看 `<Primetime DRM Key Server>/configs` PKCS 11配置檔案示例的目錄。 有關格式的資訊 [!DNL pkcs11.cfg]，請參見Sun PKCS11提供程式文檔。

要驗證HSM和Sun PKCS11配置檔案是否配置正確，可以使用以下命令： [!DNL pkcs11.cfg] 檔案所在位置( [!DNL keytool] 隨Java JRE和JDK一起安裝):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果在清單中看到您的憑據，則HSM配置正確，密鑰伺服器將能夠訪問憑據。

## 密鑰伺服器配置檔案 {#key-server-configuration-files}

黃金時段DRM密鑰伺服器需要兩種類型的配置檔案：

* 全局配置檔案， [!DNL flashaccess-keyserver-global.xml]
* 每個租戶的租戶配置檔案， [!DNL flashaccess-keyserver-tenant.xml]

如果對配置檔案進行了更改，則必須重新啟動伺服器才能使更改生效。

為避免在配置檔案中以明文方式提供密碼，必須對全局配置檔案和租戶配置檔案中指定的所有密碼進行加密。 有關加密密碼的詳細資訊，請參見 [*密碼加擾器* 在 *使用黃金時段DRM伺服器進行受保護的流處理*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md)。

## 配置目錄結構 {#configuration-directory-structure}

配置目錄具有以下結構：

```
KeyServer.ConfigRoot/  
--flashaccess-keyserver-global.xml 
--pkcs11.cfg (optional) 
--faxsks/ 
----tenants/ 
------tenantname/
---------flashaccess-keyserver-tenant.xml 
---------credential.pfx (optional) 
```

## 全局配置檔案 {#global-configuration-file}

的 [!DNL flashaccess-keyserver-global.xml] 配置檔案包含適用於密鑰伺服器的所有租戶的設定。 此檔案必須位於 `KeyServer.ConfigRoot`。 查看 [!DNL configs] 的子目錄。 全局配置檔案包括以下內容：

* 日誌記錄 — 指定日誌記錄級別和滾動日誌檔案的頻率。
* HSM密碼 — 僅當使用HSM儲存伺服器憑據時才需要。

請參閱位於 `<Primetime DRM Key Server>/configs` 的子菜單。

## 租戶配置檔案 {#tenant-configuration-files}

的 [!DNL flashaccess-ioskeyserver-tenant.xml] 和 [!DNL flashaccess-xboxkeyserver-tenant.xml] 配置檔案包含適用於黃金時段DRM密鑰伺服器的特定租戶的設定。 每個租戶都有其自己的這些配置檔案實例位於 [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]。 查看 [!DNL configs/faxsks/tenants/sampletenant] 的子目錄。

可以將租戶配置檔案中的所有檔案路徑指定為相對於租戶配置目錄的絕對路徑或路徑( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname])。

所有租戶配置檔案包括：

* 密鑰伺服器憑據 — 指定由Adobe頒發的一個或多個密鑰伺服器憑據（證書和私鑰）。 可以指定為指向 [!DNL .pfx] 檔案和密碼，或HSM上儲存的憑據的別名。 可以在此處指定幾種此類憑據，它們可以是檔案路徑或密鑰別名，也可以是兩者。

的 **iOS** 租戶配置檔案包括：

* 密鑰傳遞窗口 — （可選）指定密鑰傳遞請求時間戳有效性窗口（秒）。 預設值為500秒。

的 **Xbox 360** 租戶配置檔案包括：

* XSTS憑據 — 指定用於解密XSTS令牌的應用程式開發者的憑據
* XSTS簽名證書 — 指定用於驗證XSTS令牌上簽名的證書。
* Packager Allow清單 — 密鑰伺服器信任的Packager證書。 如果清單中沒有包裝程式證書，則所有打包程式證書都將受信任。

## 日誌檔案 {#log-files}

由Mogfire DRM密鑰伺服器應用程式( [!DNL flashaccess-ioskeyserver_*.log] 和 [!DNL flashaccess-xboxkeyserver_*.log])將位於由指定的目錄中 `KeyServer.LogRoot`。

日誌檔案按客戶端類型進行區分。 每個客戶端類型有兩個日誌：

* 安 *訪問日誌*  — 僅監視請求和響應。
* A *上下文日誌*  — 包含詳細的錯誤消息和堆棧跟蹤。

## 啟動密鑰伺服器 {#starting-the-key-server}

要啟動密鑰伺服器，請啟動Tomcat。
