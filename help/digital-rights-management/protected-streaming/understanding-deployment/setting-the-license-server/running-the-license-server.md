---
title: 運行用於受保護流的DRM伺服器
description: 運行用於受保護流的DRM伺服器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# 運行用於受保護流的DRM伺服器{#running-the-drm-server-for-protected-streaming}

在啟動Adobe PrimetimeDRM Server for Protected Streaming之前，建議您驗證配置檔案中設定的有效性。

您可以使用隨授權伺服器提供的公用程式來驗證設定的有效性。 (請參見本指南中的&#x200B;*配置驗證器*。

如果要啟動Tomcat和許可證伺服器，則需要從Tomcat的[!DNL bin]目錄運行[!DNL catalina.bat start]或[!DNL catalina.sh start]。

啟動伺服器後，您需要通過在瀏覽器窗口中開啟`https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1`來驗證是否已正確配置。 如果租用戶設定已成功載入，則會顯示確認訊息。

## 日誌檔案{#log-files}

由Adobe PrimetimeDRM Server for Protected Streaming應用程式生成的日誌檔案位於LicenseServer.LogRoot指定的目錄中。

>[!NOTE]
>
>如果當前日誌檔案在伺服器運行時被刪除或移動，則不能重新建立日誌檔案。 因此，某些日誌資訊可能會被刪除。

### 日誌目錄結構{#section_F490A483D60145ADBC21038914C39203}

日誌目錄的結構化是為了便於使用。 日誌目錄具有以下結構：

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

### 全局日誌檔案{#section_1CFA90748142439C9F3BE380969539DA}

全局日誌檔案[!DNL flashaccess-global.log]位於&#x200B;*LicenseServer.LogRoot*&#x200B;中。 日誌可以包括在伺服器初始化期間Adobe PrimetimeDRM Java SDK或日誌消息可能已生成的日誌消息。

### 分區日誌檔案{#section_5660137CD6AA40519E72A4315534846B}

分區日誌檔案[!DNL flashaccess-partition.log]位於`<LicenseServer.LogRoot>/flashaccesserver`目錄中。 它包含在處理授權要求期間產生的記錄訊息。

### 租用戶日誌檔案{#section_F0257CC0831647F18A746B4F02E3E910}

每個租用戶的租用戶日誌檔案[!DNL flashaccess-tenant.log]位於`<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`中。 租用戶記錄包含稽核資訊，說明為此租用戶產生的每個授權。

## 更新配置檔案{#updating-configuration-files}

一旦許可證伺服器讀取其中一個許可證伺服器配置檔案（全局或租用戶配置），配置資訊就快取在記憶體中。 因此，每個授權要求都不需要從磁碟讀取檔案。 但是，伺服器還允許修改配置檔案中的大部分值，而無需伺服器重新啟動即可使更改生效。

每當您修改配置檔案時，許可證伺服器都會儲存上次修改檔案的時間。 在可配置的時間間隔內，伺服器檢查檔案修改時間是否已更改。 如果更改了，伺服器會自動重新載入配置檔案的內容。

如果要控制伺服器檢查更新的頻率，您需要在全局配置檔案的`Caching`元素中設定`refreshDelaySeconds`屬性。 例如，如果`refreshDelaySeconds`設為3600秒，則伺服器將在設定檔案修改時間起算的最多一小時內更新設定。 如果`refreshDelaySeconds`設為0，則伺服器會在每次要求時檢查組態更新。 不建議您在任何生產環境中將`refreshDelaySeconds`設為低值，因為這樣做會影響效能。

`Caching`元素也控制一次快取多少租戶的設定。 您可以將此值設定為小於租戶總數的數字，以限制用於快取配置資訊的記憶體量。 如果收到非快取中租用戶的要求，在處理要求之前先載入設定。 如果快取已滿，則會從快取中移除最近最少使用的租用戶。

快取版本的組態會持續用於下列情況（直到下次伺服器檢查更新為止）:

* 如果在伺服器嘗試讀取檔案時，將更改保存到配置檔案或[!DNL flashaccess-tenant.xml]檔案中引用的任何證書檔案
* 如果發現檔案的時間戳記在當前時間之前不到一秒
* 如果檔案的時間戳記是將來

如果沒有快取版本，則載入設定會失敗，並傳回錯誤給用戶端。 然後，伺服器會在下次收到該租用戶的要求時，再次嘗試載入檔案。

### 更新全局配置檔案{#section_AA546C72442646CFB8906AEEBDF50587}

您可以隨時在[!DNL flashaccess-global.xml]中修改HSM密碼。 這些更改將在伺服器下次重新載入配置檔案時生效。 不過，「記錄」和「快取」元素的變更不會重新載入。 您需要在這些元素的任何更改生效之前重新啟動伺服器。

### 更新租用戶配置檔案{#section_71624DB8DF28480F84F34F0FF7FD4365}

您可以隨時修改在[!DNL flashaccess-tenant.xml]檔案中指定的所有值。 這些更改將在伺服器下次重新載入配置檔案時生效。 此外，伺服器檢查所有憑證([!DNL .pfx])檔案中是否有任何修改，並允許清單證書檔案在租用戶配置檔案中引用。