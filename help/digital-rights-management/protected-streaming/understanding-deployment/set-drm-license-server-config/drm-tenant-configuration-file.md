---
description: Flashaccess-tenant.xml組態檔包含套用至授權伺服器特定租用戶的設定。
seo-description: Flashaccess-tenant.xml組態檔包含套用至授權伺服器特定租用戶的設定。
seo-title: 租用戶配置檔案
title: 租用戶配置檔案
uuid: bc9ee4a1-63b6-4362-9929-3e9fe8251075
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# 租用戶配置檔案{#tenant-configuration-file}

Flashaccess-tenant.xml組態檔包含套用至授權伺服器特定租用戶的設定。

每個租用戶都支援其中的此配置檔案實例 `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`。 請參閱目 `configs/flashaccessserver/tenants/sampletenant` 錄以取得租用戶設定檔案的範例。

您可以指定租用戶設定檔案中的所有檔案路徑為絕對路徑或相對於租用戶設定目錄(`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`)的路徑。

租用戶配置檔案包括：

* *傳輸憑證* — 指定Adobe核發的一或多個傳輸憑證（憑證和私密金鑰）。 可以指定為檔案和口令 [!DNL .pfx] 的路徑，或儲存在HSM上的憑據的別名。 可以在此處指定數個此類憑據，可以是檔案路徑或密鑰別名，也可以是兩者。

   如需 *需額外認證* ，請參 *閱使用Adobe Primetime DRM SDK for Protecting Content* ，以取得更多相關資訊。

* *授權伺服器憑證* — 指定Adobe所核發的一或多個授權伺服器憑證（憑證和私密金鑰）。 您可以指定許可證伺服器憑據作為檔案和密 [!DNL .pfx] 碼的路徑，或者作為儲存在HSM上的憑據的別名。 可以在此處指定數個此類憑據，可以是檔案路徑或密鑰別名，也可以是兩者。

   如需 *需額外認證* ，請參 *閱使用Adobe Primetime DRM SDK for Protecting Content* ，以取得更多相關資訊。

* *密鑰伺服器證書* — （可選）指定Adobe所核發之Key Server授權伺服器憑證。 您可以指定密鑰伺服器的許可證伺服器證書作為檔案路徑或 [!DNL .cer] 儲存在HSM上的證書的別名。 必須指定此選項，才能為隨DRM政策封裝的內容發放授權，該政策要求iOS裝置需要遠端金鑰傳送。

* *自訂授權者* — （可選）指定自訂授權者類別，以針對每個授權要求進行叫用。 如果指定多個授權者，則會依所列順序叫用。
* *授權封裝器清單* — （可選）指定證書，用於標識有權為此許可證伺服器打包內容的實體。 如果未指定封裝程式憑證，伺服器會針對任何封裝程式所封裝的內容發行授權。 如果伺服器收到來自未授權打包程式的許可請求，則拒絕該請求。
* *支援的最低用戶端版本* ，請參閱使用Adobe Primetime DRM SDK保護內容。

* *使用規則*

   * *授權快取* — （可選）指定在用戶端上儲存授權的時間。 依預設會停用授權快取。 如果您想在限定的時段內啟用授權快取，您必須設定應儲存授權的結束日期或秒數（從核發授權時開始）。 將秒數設為0會停用授權快取。

      >[!NOTE]
      >
      >「保護串流伺服器」所核發的所有授權都包含24小時（86400秒）的有效期。 此值會隱式套用為上界，適用於為授權快取設定的任何結束日期或持續時間，最大值為86400秒，即使架構會強制執行較高的界限。

   * *正確播放* — 必須至少指定一項權利。 如果您指定多個權限，則客戶會使用第一個符合所有要求的權限。

      * *輸出保護* — 控制輸出至外部轉換裝置是否應受到保護。
      * *AIR和SWF應用程式限制* — 可選的允許清單列出可播放內容的SWF和AIR應用程式（例如，僅允許指定的應用程式）。 SWF應用程式可透過URL或SWF摘要識別，以及允許下載和驗證摘要的最長時間。

         如需如 *何計算SWF摘要的詳細資訊* ，請參閱SWF雜湊計算器。

         發行者ID和選用的應用程式ID、最低版本和最高版本可識別AIR和iOS應用程式。 如果您未指定任何應用程式限制，則任何SWF或AIR應用程式都可播放內容。

      * *DRM和Runtime模組限制* — 指定DRM/Runtime模組所需的最低安全級別。 可選地包括不允許播放內容的版本的塊清單。 模組版本由屬性標識，如作業系統和／或版本號。

         DRM模組限制和執行時期模組限制現在支援下列其他屬性：

         * `oemVendor`
         * `model`
         * `screenType`

         下列屬性現在為選用：

         * `osVersion`
         * `version`
      * *裝置功能需求* — （可選）指定訪問內容所需的硬體功能。
      * *越獄檢測要求* — （可選）指定不允許在檢測到越獄的設備上播放。



如需詳細資訊，請參閱範例租用戶設定檔案中的註解。
