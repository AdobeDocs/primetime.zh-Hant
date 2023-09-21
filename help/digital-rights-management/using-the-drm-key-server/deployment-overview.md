---
title: 部署Primetime DRM金鑰伺服器概述
description: 部署Primetime DRM金鑰伺服器概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# 部署Primetime DRM金鑰伺服器 {#deploy-the-primetime-drm-key-server}

部署Primetime DRM Key Server之前，請確定您已安裝必要的Java和Tomcat版本。 請參閱， [DRM關鍵伺服器需求](../../digital-rights-management/using-the-drm-key-server/requirements.md).

Primetime DRM金鑰伺服器下載包括 [!DNL faxsks.war]. 若要部署此WAR檔案，請將檔案複製到 [!DNL webapps] 目錄。 如果您先前已經部署WAR檔案，您可能需要手動刪除解壓縮的WAR目錄。 [!DNL faxsks] 在Tomcat中 [!DNL webapps] 目錄)。 若要防止Tomcat解壓縮WAR檔案，請編輯 [!DNL server.xml] Tomcat中的檔案 [!DNL conf] 目錄並設定 `unpackWARs` 歸因至 `false`.

Primetime DRM金鑰伺服器可選擇使用平台專屬的程式庫(`jsafe.dll` 在Windows或 `libjsafe.so` 在Linux上)以提升效能。 從複製您平台的適當程式庫 `thirdparty/cryptoj/platform` 至指定的位置 `PATH` 環境變數(或 `LD_LIBRARY_PATH` 在Linux上)。

>[!NOTE]
>
>64位元版本的 [!DNL jsafe] 若作業系統和JDK都支援64位元，才應該使用程式庫，否則請使用32位元版本。

## SSL設定 {#ssl-configuration}

遠端HTTPS金鑰傳遞需要SSL。 SSL連線可由應用程式伺服器處理（即透過在Tomcat中設定SSL），或可在其他伺服器處理（即負載平衡器、SSL加速器或Apache）。 遠端HTTPS金鑰傳遞需要SSL連線。 伺服器需要由受信任的CA核發的SSL憑證。

設定SSL有多種選項。 以下範例說明如何在Apache和Tomcat中設定具有使用者端驗證的SSL。

以下範例顯示Apache SSL設定：

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

下列範例顯示Tomcat SSL設定。 若要產生憑證和金鑰檔案：

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

提示輸入一般名稱時，請使用伺服器的完整網域名稱(FQDN)。

複製 [!DNL server.cer]、和 [!DNL server.key] 到Tomcat目錄。 在中指定下列聯結器 [!DNL conf/server.xml]：

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

您可以選擇設定下列兩個Java系統屬性，以修改Primetime DRM Key Server的組態和記錄檔位置：

* `KeyServer.ConfigRoot`  — 此目錄包含Primetime DRM Key Server的所有組態檔。 如需這些檔案內容的詳細資訊，請參閱 [金鑰伺服器組態檔](#key-server-configuration-files). 如果未設定，預設值為 [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot`  — 這是包含iOS金鑰伺服器應用程式記錄的記錄目錄。 若未設定，則預設為與 `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot`  — 這是包含Xbox Key Server應用程式日誌的日誌目錄。 若未設定，預設值會與 `KeyServer.ConfigRoot`.

如果您使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 若要啟動Tomcat，可以使用 `JAVA_OPTS` 環境變數。 啟動Tomcat時，將使用此處設定的任何Java選項。 例如，設定：

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM認證 {#primetime-drm-credentials}

若要處理來自Primetime DRM iOS和Xbox 360使用者端的金鑰要求，Primetime DRM金鑰伺服器必須設定一組由Adobe簽發的認證。 這些憑證可以儲存在PKCS#12 ( [!DNL .pfx])檔案或HSM上。

此 [!DNL .pfx] 檔案可位於任何位置，但為方便設定，Adobe建議將檔案放置在 [!DNL .pfx] 租使用者設定目錄中的檔案。 如需詳細資訊，請參閱 [金鑰伺服器組態檔](#key-server-configuration-files).

### HSM組態 {#section_13A19E3E32934C5FA00AEF621F369877}

如果您選擇使用HSM來儲存伺服器認證，則必須將私密金鑰和憑證載入到HSM上，並建立 *pkcs11.cfg* 組態檔。 此檔案必須位於 *KeyServer.ConfigRoot* 目錄。 請參閱 `<Primetime DRM Key Server>/configs` PKCS 11組態檔範例的目錄。 如需格式化的詳細資訊， [!DNL pkcs11.cfg]，請參閱Sun PKCS11提供者檔案。

若要確認您的HSM和Sun PKCS11組態檔已正確設定，您可以使用以下目錄中的指令： [!DNL pkcs11.cfg] 檔案位於( [!DNL keytool] （隨Java JRE和JDK安裝）：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您在清單中看到您的認證，則HSM已正確設定，金鑰伺服器將能夠存取認證。

## 金鑰伺服器組態檔 {#key-server-configuration-files}

Primetime DRM Key Server需要兩種組態檔：

* 全域組態檔， [!DNL flashaccess-keyserver-global.xml]
* 每個租使用者的租使用者設定檔， [!DNL flashaccess-keyserver-tenant.xml]

如果對組態檔進行了變更，則必須重新啟動伺服器，變更才會生效。

為了避免在設定檔案中以純文字提供密碼，必須加密全域和租使用者設定檔案中指定的所有密碼。 如需加密密碼的詳細資訊，請參閱 [*密碼加擾器* 在 *使用受保護串流的Primetime DRM伺服器*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## 設定目錄結構 {#configuration-directory-structure}

組態目錄的結構如下：

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

## 全域設定檔 {#global-configuration-file}

此 [!DNL flashaccess-keyserver-global.xml] 組態檔包含套用至Key Server所有租使用者的設定。 此檔案必須位於 `KeyServer.ConfigRoot`. 請參閱 [!DNL configs] 範例全域組態檔的目錄。 全域組態檔包含下列專案：

* 記錄 — 指定記錄層級以及記錄檔的捲動頻率。
* HSM密碼 — 只有在使用HSM儲存伺服器憑證時才需要。

請參閱位於下列位置的範例全域組態檔中的註解： `<Primetime DRM Key Server>/configs` 以取得更多詳細資料。

## 租使用者組態檔 {#tenant-configuration-files}

此 [!DNL flashaccess-ioskeyserver-tenant.xml] 和 [!DNL flashaccess-xboxkeyserver-tenant.xml] 組態檔包含套用至Primetime DRM Key Server之特定租使用者的設定。 每個租使用者都有其自己的這些設定檔案例項，位於 [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. 請參閱 [!DNL configs/faxsks/tenants/sampletenant] 範例租使用者組態檔的目錄。

您可以將租使用者設定檔案中的所有檔案路徑指定為絕對路徑或相對於租使用者設定目錄的路徑( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname])。

所有租使用者組態檔都包括：

* 金鑰伺服器認證 — 指定一或多個Adobe發行的金鑰伺服器認證（憑證和私密金鑰）。 可以指定為 [!DNL .pfx] 檔案和密碼，或儲存在HSM上的認證別名。 您可以在此處指定數個這類認證，作為檔案路徑或金鑰別名，或同時指定兩者。

此 **iOS** 租使用者設定檔包含：

* 金鑰傳遞期間 — （選用）指定金鑰傳遞請求時間戳記有效期間（以秒為單位）。 預設值為500秒。

此 **Xbox 360** 租使用者設定檔包含：

* XSTS認證 — 指定用來解密XSTS權杖的應用程式開發人員認證
* XSTS簽署憑證 — 指定用來驗證XSTS權杖上簽章的憑證。
* 封裝程式允許清單 — 金鑰伺服器信任的封裝程式憑證。 如果清單中沒有封裝者憑證，則會信任所有封裝者憑證。

## 記錄檔 {#log-files}

Primetime DRM金鑰伺服器應用程式產生的記錄檔( [!DNL flashaccess-ioskeyserver_*.log] 和 [!DNL flashaccess-xboxkeyserver_*.log])將位於指定的目錄中 `KeyServer.LogRoot`.

記錄檔可依使用者端型別加以區分。 每種使用者端型別有兩個記錄：

* 一個 *存取記錄*  — 僅監視請求和回應。
* A *內容記錄*  — 包含詳細的錯誤訊息和棧疊追蹤。

## 啟動金鑰伺服器 {#starting-the-key-server}

若要啟動金鑰伺服器，請啟動Tomcat。
