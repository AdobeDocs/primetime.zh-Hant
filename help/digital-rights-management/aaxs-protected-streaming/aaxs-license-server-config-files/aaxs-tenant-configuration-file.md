---
title: 租用戶配置檔案
description: 租用戶配置檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# 租用戶配置檔案{#tenant-configuration-file}

Flashaccess-tenant.xml設定檔包含套用至授權伺服器特定租用戶的設定。 每個租用戶在&#x200B;*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*&#x200B;中都有自己的此配置檔案實例。 如需租用戶設定檔案的範例，請參閱[!DNL configs/flashaccessserver/tenants/sampletenant]目錄。

您可以指定租用戶配置檔案中的所有檔案路徑作為相對於租用戶配置目錄的絕對路徑或路徑(*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*)。

租用戶配置檔案包括：

* **傳輸憑證** — 指定由Adobe頒發的一個或多個傳輸憑據（證書和私鑰）。可以指定為。pfx檔案和口令的路徑，或儲存在HSM上的憑據的別名。 可以在此處指定數個此類憑據，可以是檔案路徑或密鑰別名，也可以是兩者。 如需需要額外憑證的詳細資訊，請參閱&#x200B;*使用Adobe存取SDK保護內容中的「處理憑證更新[」。](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)*
* **授權伺服器憑證** — 指定由Adobe核發的一或多個授權伺服器憑證（憑證和私密金鑰）。可以指定為。pfx檔案和口令的路徑，或儲存在HSM上的憑據的別名。 可以在此處指定數個此類憑據，可以是檔案路徑或密鑰別名，也可以是兩者。 如需需要額外認證的詳細資訊，請參閱「使用Adobe存取SDK保護內容」*中的「處理認證更新」。
* **密鑰伺服器證書** — 可選。指定由Adobe頒發的密鑰伺服器許可證伺服器證書。 可以指定為。cer檔案的路徑或儲存在HSM上的證書的別名。 必須指定此選項，才能為使用要求iOS裝置遠端密鑰傳送之原則封裝的內容發行授權。
* **自訂授權者** — 可選。指定要針對每個授權要求叫用的自訂授權者類別。 如果指定多個授權者，則會依所列順序叫用。 如需詳細資訊，請參閱「[自訂授權擴充功能](../../aaxs-protected-streaming/custom-authorization-extensions.md)」。
* **授權封裝器清單** — 可選。指定證書，用於標識有權為此許可證伺服器打包內容的實體。 如果未指定封裝程式憑證，伺服器會針對任何封裝程式所封裝的內容發行授權。
* **最低支援的用戶端版本** (請 *參閱使用Adobe存取SDK來保護內容*)。
* **使用規則**

   * **授權快取** — 可選。指定許可證可以儲存在客戶機上的時間。 依預設會停用授權快取。 若要啟用有限時段的授權快取，請設定應儲存授權的結束日期或秒數（從發放授權時開始）。 將秒數設為0會停用授權快取。

      請注意，伺服器針對受保護串流所核發的所有授權的有效期為24小時（86400秒）。 因此，此值會隱式套用為上限，以便套用至為授權快取設定的任何結束日期或持續時間，最大值為86400秒，即使架構會強制執行較高的界限。

   * **正確播放** — 至少必須指定一項權利。如果指定多個權限，客戶會使用第一個符合所有要求的權限。

      * **輸出保護** — 控制輸出至外部轉換裝置是否應受到保護。
      * **AIR和SWF應用程式限制** — 可選的允許清單列出可播放內容的SWF和AIR應用程式（亦即僅允許指定的應用程式）。SWF應用程式可透過URL或SWF摘要識別，並允許下載和驗證摘要的最長時間。 如需有關計算SWF摘要的詳細資訊，請參閱「SWF雜湊計算器」一節。 AIR和iOS應用程式由發行者ID和選用的應用程式ID、最低版本和最高版本識別。 如果未指定任何應用程式限制，則任何SWF或AIR應用程式都可能播放內容。
      * **DRM和Runtime模組限制** — 指定DRM/Runtime模組所需的最低安全級別。可選地包括不允許播放內容的版本的塊清單。 模組版本由諸如作業系統和／或版本號等屬性標識。 DRM模組限制和執行時期模組限制現在支援下列其他屬性：

         * `oemVendor`
         * `model`
         * `screenType`

         下列屬性現在為選用：

         * `osVersion`
         * `version`
      * **裝置功能需求** — （可選）指定訪問內容所需的硬體功能。
      * **越獄檢測要求** — （可選）指定不允許在檢測到越獄的設備上播放。



如需詳細資訊，請參閱範例租用戶設定檔案中的註解。
