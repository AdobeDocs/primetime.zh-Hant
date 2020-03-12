---
seo-title: 部署Primetime DRM Key Server概觀
title: 部署Primetime DRM Key Server概觀
uuid: 86630675-c15d-4f32-8212-d7343f4f92e0
translation-type: tm+mt
source-git-commit: 105dedcfe47a5f454a067e66a95827e638290742

---


# 部署Primetime DRM Key Server {#deploy-the-primetime-drm-key-server}

在部署Primetime DRM Key Server之前，請確定您已安裝必要版本的Java和Tomcat。 請參閱「 [DRM主要伺服器需求」](../../digital-rights-management/using-the-drm-key-server/requirements.md)。

Primetime DRM Key Server下載包括 [!DNL faxsks.war]。 要部署此WAR檔案，請將該檔案複製到Tomcat的目 [!DNL webapps] 錄。 如果先前已部署了WAR檔案，則可能需要手動刪除Tomcat目錄 [!DNL faxsks] 中未打包的WAR [!DNL webapps] 目錄。 為防止Tomcat解壓縮WAR檔案，請編 [!DNL server.xml] 輯Tomcat目錄中的 [!DNL conf] 檔案，並將屬 `unpackWARs` 性設定為 `false`。

Primetime DRM Key Server可選擇使用平台特定的程式庫(`jsafe.dll` 在Windows或 `libjsafe.so` 在Linux上)來改善效能。 將適合您平台的程式庫從環 `thirdparty/cryptoj/platform` 境變數（或在Linux上）所 `PATH` 指定的位 `LD_LIBRARY_PATH` 置複製到。

>[!NOTE]
>
>只有當作業系統和JDK都支 [!DNL jsafe] 援64位元時，才應使用64位元版本的程式庫，否則應使用32位元版本。

## SSL設定 {#ssl-configuration}

遠端HTTPS金鑰傳送需要SSL。 SSL連線可由應用程式伺服器處理（即，在Tomcat中設定SSL），或可在其他伺服器（例如負載平衡器、SSL加速器或Apache）處理。 遠端HTTPS金鑰傳送需要SSL連線。 伺服器需要由受信任的CA頒發的SSL證書。

設定SSL有多種選項。 以下是在Apache和Tomcat中使用用戶端驗證來設定SSL的範例。

下列範例顯示Apache SSL組態：

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

以下示例顯示了Tomcat SSL配置。 要生成證書和密鑰檔案，請執行以下操作：

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

當提示輸入公用名稱時，請使用伺服器的完全限定域名(FQDN)。

復 [!DNL server.cer]制並 [!DNL server.key] 複製到Tomcat目錄。 在中指定以下連接器 [!DNL conf/server.xml]:

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

您可以選擇設定以下兩個Java系統屬性來修改Primetime DRM密鑰伺服器的配置和日誌檔案位置：

* `KeyServer.ConfigRoot` -此目錄包含Primetime DRM密鑰伺服器的所有配置檔案。 有關這些檔案內容的詳細資訊，請參 [閱Key Server配置檔案](#key-server-configuration-files)。 如果未設定，則預設值為 [!DNL CATALINA_BASE/keyserver]。

* `KeyServer.LogRoot` -此日誌目錄包含iOS Key Server應用程式日誌。 如果未設定，則預設值與 `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` -此為包含Xbox Key Server應用程式記錄檔的記錄檔目錄。 如果未設定，則預設值與相同 `KeyServer.ConfigRoot`。

如果使用或 [!DNL catalina.bat] 啟 [!DNL catalina.sh] 動Tomcat，則可使用環境變數輕鬆設定這些系統 `JAVA_OPTS` 屬性。 在啟動Tomcat時，將使用此處設定的任何Java選項。 例如，設定：

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM認證 {#primetime-drm-credentials}

若要處理來自Primetime DRM iOS和Xbox 360用戶端的金鑰要求，Primetime DRM金鑰伺服器必須配置有Adobe核發的一組認證。 這些憑據可以儲存在PKCS#12( [!DNL .pfx])檔案或HSM中。

檔 [!DNL .pfx] 案可隨處取用，但為方便設定，Adobe建議將檔案置 [!DNL .pfx] 於租用戶的設定目錄中。 如需詳細資訊，請參 [閱Key Server設定檔](#key-server-configuration-files)。

### HSM配置 {#section_13A19E3E32934C5FA00AEF621F369877}

如果您選擇使用HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立 *pkcs11.cfg* 配置檔案。 此檔案必須位於 *KeyServer.ConfigRoot目錄中* 。 請參閱 [!DNL <Primetime DRM Key Server>/configs目錄] ，用於示例PKCS 11配置檔案。 有關格式的資訊 [!DNL pkcs11.cfg]，請參見Sun PKCS11提供程式文檔。

要驗證HSM和Sun PKCS11配置檔案是否已正確配置，可以從檔案所在的目錄（隨Java JRE和JDK一起安裝）中使用 [!DNL pkcs11.cfg][!DNL keytool] 以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您在清單中看到憑據，則HSM已正確配置，密鑰伺服器將能夠訪問憑據。

## 關鍵伺服器配置檔案 {#key-server-configuration-files}

Primetime DRM Key Server需要兩種類型的配置檔案：

* 全局配置檔案， [!DNL flashaccess-keyserver-global.xml]
* 每個租用戶的租用戶配置檔案， [!DNL flashaccess-keyserver-tenant.xml]

如果對配置檔案進行了更改，則必須重新啟動伺服器才能使更改生效。

為避免在配置檔案中以明文形式提供密碼，必須加密全局配置檔案和租用戶配置檔案中指定的所有密碼。 如需加密密碼的詳細資訊，請參 [*閱使用Primetime DRM *Server*&#x200B;進行受保護串流的密碼剪貼器&#x200B;*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md)。

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

配置 [!DNL flashaccess-keyserver-global.xml] 檔案包含適用於密鑰伺服器的所有租戶的設定。 此檔案必須位於中 `KeyServer.ConfigRoot`。 有關全 [!DNL configs] 局配置檔案示例，請參見目錄。 全域設定檔包含下列項目：

* 記錄——指定記錄級別以及記錄檔案的滾動頻率。
* HSM密碼——僅當使用HSM儲存伺服器憑據時才需要。

請參閱位於 [!DNL <Primetime DRM Key Server>/configs] ，以瞭解詳細資訊。

## 租用戶設定檔案 {#tenant-configuration-files}

該和 [!DNL flashaccess-ioskeyserver-tenant.xml] 配 [!DNL flashaccess-xboxkeyserver-tenant.xml] 置檔案包含適用於Primetime DRM密鑰伺服器的特定租用戶的設定。 每個租用戶都有其自己的這些配置檔案實例位於 [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]。 請參閱目 [!DNL configs/faxsks/tenants/sampletenant] 錄以取得租用戶設定檔案的範例。

您可以指定租用戶設定檔案中的所有檔案路徑為相對於租用戶設定目錄( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname])的絕對路徑或路徑。

所有租用戶配置檔案包括：

* 金鑰伺服器憑證——指定Adobe所核發的一或多個金鑰伺服器憑證（憑證和私密金鑰）。 可以指定為檔案和口令 [!DNL .pfx] 的路徑，或儲存在HSM上的憑據的別名。 可以在此處指定數個此類憑據，可以是檔案路徑或密鑰別名，也可以是兩者。

iOS租 **用戶** 設定檔包含：

* 關鍵傳送窗口-（可選）指定關鍵傳送請求時間戳有效性窗口（以秒為單位）。 預設值為500秒。

**Xbox 360租用戶組態檔** ，包含：

* XSTS憑證——指定用於解密XSTS Token的應用程式開發人員憑證
* XSTS簽署憑證——指定用來驗證XSTS Token上簽名的憑證。
* Packager白名單——密鑰伺服器信任的Packager證書。 如果清單中沒有包裝器證書，則所有包裝器證書都將受信任。

## 日誌檔案 {#log-files}

由Primetime DRM Key Server應用程式( [!DNL flashaccess-ioskeyserver_*.log] 和 [!DNL flashaccess-xboxkeyserver_*.log])產生的記錄檔將位於指定的目錄中 `KeyServer.LogRoot`。

日誌檔案按客戶端類型區分。 每個客戶端類型有兩個日誌：

* 存 *取記錄* -僅監視請求和回應。
* 上下文 *日誌* -包含詳細的錯誤消息和堆棧跟蹤。

## 啟動密鑰伺服器 {#starting-the-key-server}

要啟動Key Server，請啟動Tomcat。