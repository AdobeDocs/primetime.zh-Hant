---
title: 運行DRM伺服器以進行受保護的流處理
description: 運行DRM伺服器以進行受保護的流處理
copied-description: true
exl-id: 05dc4c55-a97e-4bdc-aea8-32741299454c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# 運行DRM伺服器以進行受保護的流處理 {#running-the-drm-server-for-protected-streaming}

在啟動用於受保護流的Adobe PrimetimeDRM伺服器之前，建議您驗證配置檔案中設定的有效性。

您可以使用隨許可證伺服器提供的實用程式來驗證設定的有效性。 (請參閱 *配置驗證程式* 的子菜單。

如果要啟動Tomcat和許可證伺服器，需要運行 [!DNL catalina.bat start] 或 [!DNL catalina.sh start] 從Tomcat [!DNL bin] 的子菜單。

伺服器啟動後，您需要通過開啟來驗證是否已正確配置 `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1` 按鈕。 如果租戶配置已成功載入，則會顯示確認消息。

## 日誌檔案 {#log-files}

由Adobe PrimetimeDRM伺服器為受保護的流式處理應用程式生成的日誌檔案位於LicenseServer.LogRoot指定的目錄中。

>[!NOTE]
>
>如果當前日誌檔案在伺服器運行時被刪除或移動，則不能重新建立日誌檔案。 因此，可能會刪除一些日誌資訊。

### 日誌目錄結構 {#section_F490A483D60145ADBC21038914C39203}

日誌目錄是為便於使用而構建的。 日誌目錄具有以下結構：

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

### 全局日誌檔案 {#section_1CFA90748142439C9F3BE380969539DA}

全局日誌檔案， [!DNL flashaccess-global.log]，位於 *LicenseServer.LogRoot*。 該日誌可包括Adobe PrimetimeDRM Java SDK或日誌消息在伺服器初始化期間可能已生成的日誌消息。

### 分區日誌檔案 {#section_5660137CD6AA40519E72A4315534846B}

分區日誌檔案， [!DNL flashaccess-partition.log]的 `<LicenseServer.LogRoot>/flashaccesserver` 的子菜單。 它包括在處理許可證請求期間生成的日誌消息。

### 租戶日誌檔案 {#section_F0257CC0831647F18A746B4F02E3E910}

每個租戶的租戶日誌檔案， [!DNL flashaccess-tenant.log]，位於 `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`。 租戶日誌包括描述為此租戶生成的每個許可證的審核資訊。

## 正在更新配置檔案 {#updating-configuration-files}

一旦許可證伺服器讀取許可證伺服器配置檔案之一（全局或租戶配置），配置資訊就被快取在記憶體中。 因此，對於每個許可證請求，都不必從磁碟讀取檔案。 但是，伺服器還允許修改配置檔案中的大多數值，而不需要伺服器重新啟動才能使更改生效。

無論何時修改配置檔案，許可證伺服器都會儲存上次修改檔案的時間。 在可配置的時間間隔內，伺服器檢查檔案修改時間是否已更改。 如果已更改，伺服器將自動重新載入配置檔案的內容。

如果要控制伺服器檢查更新的頻率，需要設定 `refreshDelaySeconds` 屬性 `Caching` 全局配置檔案的元素。 例如，如果 `refreshDelaySeconds` 設定為3600秒，伺服器將在配置檔案修改時間後最多一小時內更新配置。 如果 `refreshDelaySeconds` 設定為0時，伺服器會在每次請求時檢查配置更新。 不建議您設定 `refreshDelaySeconds` 在任何生產環境中都會降低價值，因為這樣做會影響效能。

的 `Caching` 元素還控制一次快取租戶配置的數量。 您可以將此值設定為小於租戶總數的數字，以限制用於快取配置資訊的記憶體量。 如果接收到不在快取中的租戶的請求，則在處理該請求之前載入該配置。 如果快取已滿，則從快取中刪除最近使用的最少租戶。

在以下情況下（直到下次伺服器檢查更新時為止），將繼續使用快取的配置版本：

* 如果更改保存到配置檔案或在 [!DNL flashaccess-tenant.xml] 檔案，而伺服器嘗試讀取檔案
* 如果發現檔案的時間戳小於當前時間之前的一秒
* 如果檔案的時間戳將來是

如果沒有快取版本，則載入配置失敗，並且向客戶端返回錯誤。 然後，伺服器在下次收到該租戶的請求時再次嘗試載入該檔案。

### 更新全局配置檔案 {#section_AA546C72442646CFB8906AEEBDF50587}

您可以在 [!DNL flashaccess-global.xml] 隨時。 更改將在伺服器下次重新載入配置檔案時生效。 但是，不會重新載入對日誌記錄和快取元素所做的更改。 您需要在對這些元素所做的任何更改生效之前重新啟動伺服器。

### 更新租戶配置檔案 {#section_71624DB8DF28480F84F34F0FF7FD4365}

您可以修改在 [!DNL flashaccess-tenant.xml] 檔案。 更改將在伺服器下次重新載入配置檔案時生效。 此外，伺服器會檢查所有憑據中是否有任何修改( [!DNL .pfx])檔案和打包程式允許在租戶配置檔案中引用的清單證書檔案。
