---
title: 執行DRM伺服器以進行受保護的串流
description: 執行DRM伺服器以進行受保護的串流
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# 執行DRM伺服器以進行受保護的串流 {#running-the-drm-server-for-protected-streaming}

在啟動Adobe Primetime DRM Server for Protected Streaming之前，建議您先驗證組態檔中的設定是否有效。

您可以使用許可證伺服器隨附的公用程式來驗證設定的有效性。 (請參閱 *設定驗證器* 在本指南中。

如果要啟動Tomcat和授權伺服器，您需要執行 [!DNL catalina.bat start] 或 [!DNL catalina.sh start] 從Tomcat&#39;s [!DNL bin] 目錄。

伺服器啟動後，您必須透過開啟 `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1` 在瀏覽器視窗中。 如果租使用者設定已成功載入，則會出現確認訊息。

## 記錄檔 {#log-files}

Adobe Primetime DRM Server for Protected Streaming應用程式產生的記錄檔位於LicenseServer.LogRoot指定的目錄中。

>[!NOTE]
>
>如果伺服器執行時刪除或移動目前的記錄檔，則可能無法重新建立記錄檔。 因此，可能會刪除某些記錄檔資訊。

### 記錄目錄結構 {#section_F490A483D60145ADBC21038914C39203}

記錄目錄的結構化便於使用。 記錄目錄的結構如下：

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

### 全域記錄檔 {#section_1CFA90748142439C9F3BE380969539DA}

全域記錄檔， [!DNL flashaccess-global.log]，位於 *LicenseServer.LogRoot*. 記錄檔可能包含Adobe Primetime DRM Java SDK的記錄檔訊息，或是在伺服器初始化期間產生的記錄檔訊息。

### 資料分割記錄檔 {#section_5660137CD6AA40519E72A4315534846B}

資料分割記錄檔， [!DNL flashaccess-partition.log]，位於 `<LicenseServer.LogRoot>/flashaccesserver` 目錄。 它包含在處理授權請求期間產生的日誌訊息。

### 租使用者記錄檔 {#section_F0257CC0831647F18A746B4F02E3E910}

每個租使用者的租使用者記錄檔， [!DNL flashaccess-tenant.log]，位於 `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. 租使用者記錄檔包含稽核資訊，說明為此租使用者產生的每個授權。

## 正在更新組態檔 {#updating-configuration-files}

當授權伺服器讀取其中一個授權伺服器組態檔（全域或租使用者組態）時，組態資訊就會快取到記憶體中。 因此，不需要從磁碟讀取每個授權要求的檔案。 不過，伺服器也允許修改組態檔中的大部分值，而不需要重新啟動伺服器才能讓變更生效。

無論何時修改組態檔，許可證伺服器都會儲存上次修改檔案的時間。 伺服器會以可設定的間隔檢查檔案修改時間是否已變更。 如果已經變更，伺服器會自動重新載入組態檔的內容。

如果您想要控制伺服器檢查更新的頻率，您必須設定 `refreshDelaySeconds` 中的屬性 `Caching` 全域組態檔的元素。 例如，如果 `refreshDelaySeconds` 設為3600秒，則伺服器將在修改設定檔案後最多一小時內更新設定。 如果 `refreshDelaySeconds` 設為0，則伺服器會根據每個請求檢查設定更新。 不建議您設定 `refreshDelaySeconds` 降低任何生產環境中的值，因為這樣做可能會影響效能。

此 `Caching` element也會控制一次快取多少租使用者的設定。 您可以將此值設定為小於租使用者總數的數字，以限制用於快取設定資訊的記憶體數量。 如果收到不在快取中的租使用者的請求，則會先載入設定，然後才能處理請求。 如果快取已滿，則會從快取中移除最近最少使用的租使用者。

快取版本的設定會繼續用於下列情況（直到下次伺服器檢查更新為止）：

* 如果變更儲存到組態檔或中參照的任何憑證檔 [!DNL flashaccess-tenant.xml] 在伺服器嘗試讀取檔案時讀取檔案
* 如果發現檔案的時間戳記早於目前時間不到一秒
* 如果檔案的時間戳記是在未來

如果沒有快取版本，則載入設定會失敗，並傳回錯誤給使用者端。 然後，伺服器會在下次收到該租使用者的請求時嘗試再次載入檔案。

### 更新全域設定檔 {#section_AA546C72442646CFB8906AEEBDF50587}

您可在下列位置修改HSM密碼 [!DNL flashaccess-global.xml] 隨時。 下次伺服器重新載入組態檔時，變更就會生效。 不過，不會重新載入記錄日誌和快取元素的變更。 您必須重新啟動伺服器，這些元素的任何變更才會生效。

### 更新租使用者設定檔 {#section_71624DB8DF28480F84F34F0FF7FD4365}

您可以修改所有在 [!DNL flashaccess-tenant.xml] 任何時間傳送檔案。 下次伺服器重新載入組態檔時，變更就會生效。 此外，伺服器也會檢查所有認證( [!DNL .pfx])檔案和Packager允許列出租使用者設定檔案中參照的憑證檔案。
