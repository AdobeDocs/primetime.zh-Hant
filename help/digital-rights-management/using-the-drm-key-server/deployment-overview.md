---
title: 部署Primetime DRM Key Server概觀
description: 部署Primetime DRM Key Server概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# 部署Primetime DRM密鑰伺服器{#deploy-the-primetime-drm-key-server}

在部署Primetime DRM Key Server之前，請確定您已安裝必要版本的Java和Tomcat。 請參閱[DRM Key Server Requirements](../../digital-rights-management/using-the-drm-key-server/requirements.md)。

Primetime DRM Key Server下載包含[!DNL faxsks.war]。 要部署此WAR檔案，請將檔案複製到Tomcat的[!DNL webapps]目錄。 如果先前已部署了WAR檔案，則可能需要手動刪除未打包的WAR目錄（Tomcat的[!DNL webapps]目錄中的[!DNL faxsks]）。 為防止Tomcat解壓WAR檔案，請編輯Tomcat的[!DNL conf]目錄中的[!DNL server.xml]檔案，並將`unpackWARs`屬性設定為`false`。

Primetime DRM Key Server（可選）使用平台特定的庫（Windows上的`jsafe.dll`或Linux上的`libjsafe.so`）以提高效能。 將適合您平台的程式庫從`thirdparty/cryptoj/platform`複製至`PATH`環境變數（或`LD_LIBRARY_PATH` on Linux）所指定的位置。

>[!NOTE]
>
>[!DNL jsafe]程式庫的64位元版本僅在作業系統和JDK都支援64位元時才應使用，否則應使用32位元版本。

## SSL配置{#ssl-configuration}

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

將[!DNL server.cer]和[!DNL server.key]複製到Tomcat目錄。 在[!DNL conf/server.xml]中指定以下連接器：

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Java系統屬性{#java-system-properties}

您可以選擇設定以下兩個Java系統屬性來修改Primetime DRM密鑰伺服器的配置和日誌檔案位置：

* `KeyServer.ConfigRoot` -此目錄包含Primetime DRM密鑰伺服器的所有配置檔案。有關這些檔案內容的詳細資訊，請參見[Key Server配置檔案](#key-server-configuration-files)。 如果未設定，則預設值為[!DNL CATALINA_BASE/keyserver]。

* `KeyServer.LogRoot` -此日誌目錄包含iOS Key Server應用程式日誌。如果未設定，則預設值與`KeyServer.ConfigRoot`相同

* `XboxKeyServer.LogRoot` -此為包含Xbox Key Server應用程式記錄檔的記錄檔目錄。如果未設定，則預設值與`KeyServer.ConfigRoot`相同。

如果使用[!DNL catalina.bat]或[!DNL catalina.sh]啟動Tomcat，則可以使用`JAVA_OPTS`環境變數輕鬆設定這些系統屬性。 在啟動Tomcat時，將使用此處設定的任何Java選項。 例如，設定：

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM憑據{#primetime-drm-credentials}

要處理來自Primetime DRM iOS和Xbox 360客戶端的密鑰請求，Primetime DRM密鑰伺服器必須配置有由Adobe發出的一組憑據。 這些憑據可以儲存在PKCS#12([!DNL .pfx])檔案或HSM中。

[!DNL .pfx]檔案可隨處取用，但為方便設定，Adobe建議將[!DNL .pfx]檔案放入租用戶的設定目錄。 有關詳細資訊，請參見[鍵伺服器配置檔案](#key-server-configuration-files)。

### HSM配置{#section_13A19E3E32934C5FA00AEF621F369877}

如果您選擇使用HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM上並建立&#x200B;*pkcs11.cfg*&#x200B;配置檔案。 此檔案必須位於&#x200B;*KeyServer.ConfigRoot*&#x200B;目錄中。 有關PKCS 11配置檔案示例，請參見`<Primetime DRM Key Server>/configs`目錄。 有關[!DNL pkcs11.cfg]格式的資訊，請參見Sun PKCS11提供程式文檔。

要驗證HSM和Sun PKCS11配置檔案是否已正確配置，可以從[!DNL pkcs11.cfg]檔案所在的目錄（[!DNL keytool]隨Java JRE和JDK一起安裝）使用以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您在清單中看到憑據，則HSM已正確配置，密鑰伺服器將能夠訪問憑據。

## 關鍵伺服器配置檔案{#key-server-configuration-files}

Primetime DRM Key Server需要兩種類型的配置檔案：

* 全局配置檔案[!DNL flashaccess-keyserver-global.xml]
* 每個租用戶的租用戶配置檔案[!DNL flashaccess-keyserver-tenant.xml]

如果對配置檔案進行了更改，則必須重新啟動伺服器才能使更改生效。

為避免在配置檔案中以明文形式提供密碼，必須加密全局配置檔案和租用戶配置檔案中指定的所有密碼。 如需密碼加密的詳細資訊，請參閱&#x200B;*使用保護串流的Primetime DRM伺服器*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md)&#x200B;中的&#x200B;[*密碼剪貼器*。

## 配置目錄結構{#configuration-directory-structure}

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

## 全局配置檔案{#global-configuration-file}

[!DNL flashaccess-keyserver-global.xml]配置檔案包含適用於密鑰伺服器的所有租戶的設定。 此檔案必須位於`KeyServer.ConfigRoot`中。 有關全局配置檔案的示例，請參見[!DNL configs]目錄。 全域設定檔包含下列項目：

* 記錄——指定記錄級別以及記錄檔案的滾動頻率。
* HSM密碼——僅當使用HSM儲存伺服器憑據時才需要。

如需詳細資訊，請參閱位於`<Primetime DRM Key Server>/configs`的範例全域設定檔案中的注釋。

## 租用戶配置檔案{#tenant-configuration-files}

[!DNL flashaccess-ioskeyserver-tenant.xml]和[!DNL flashaccess-xboxkeyserver-tenant.xml]配置檔案包含適用於Primetime DRM密鑰伺服器的特定租用戶的設定。 每個租用戶在[!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]中都有其自己的這些配置檔案實例。 如需租用戶設定檔案的範例，請參閱[!DNL configs/faxsks/tenants/sampletenant]目錄。

您可以指定租用戶配置檔案中的所有檔案路徑為相對於租用戶配置目錄([!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname])的絕對路徑或路徑。

所有租用戶配置檔案包括：

* 密鑰伺服器憑據——指定由Adobe頒發的一個或多個密鑰伺服器憑據（證書和私鑰）。 可以指定為[!DNL .pfx]檔案和口令的路徑，或儲存在HSM上的憑據的別名。 可以在此處指定數個此類憑據，可以是檔案路徑或密鑰別名，也可以是兩者。

**iOS**&#x200B;租用戶配置檔案包括：

* 關鍵傳送窗口-（可選）指定關鍵傳送請求時間戳有效性窗口（以秒為單位）。 預設值為500秒。

**Xbox 360**&#x200B;租用戶配置檔案包括：

* XSTS憑證——指定用於解密XSTS Token的應用程式開發人員憑證
* XSTS簽署憑證——指定用來驗證XSTS Token上簽名的憑證。
* Packager Allow list —密鑰伺服器信任的Packager證書。 如果清單中沒有包裝器證書，則所有包裝器證書都將受信任。

## 日誌檔案{#log-files}

由Primetime DRM Key Server應用程式（[!DNL flashaccess-ioskeyserver_*.log]和[!DNL flashaccess-xboxkeyserver_*.log]）生成的日誌檔案將位於`KeyServer.LogRoot`指定的目錄中。

日誌檔案按客戶端類型區分。 每個客戶端類型有兩個日誌：

* *訪問日誌* —— 僅監視請求和響應。
* A *context log* —— 包含詳細的錯誤消息和堆棧跟蹤。

## 啟動Key Server {#starting-the-key-server}

要啟動Key Server，請啟動Tomcat。