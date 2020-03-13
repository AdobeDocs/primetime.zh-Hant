---
description: 'null'
seo-description: 'null'
seo-title: 許可證伺服器屬性檔案
title: 許可證伺服器屬性檔案
uuid: 5e94ed1f-1dbf-4506-a097-183fcd5d25ef
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 許可證伺服器屬性檔案{#license-server-properties-file}

許可證伺服器引用檔案中設定的 [!DNL flashaccess-refimpl.properties] 屬性。 您可以直接參考該檔案，以取得特定值的詳細資訊，以及每個屬性的使用資訊。 在參考實施()的目錄中提 [!DNL resources] 供了完全功能的示 `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`例。

**認證** -屬性檔案包含Adobe向您發出之認證的位置設定。 您可以在檔案中使用口 [!DNL .pfx] 令指定這些憑據，或為儲存在HSM上的憑據提供別名和密碼。 您至少需要配置與傳輸憑證和許可證伺服器憑證相關的屬性。 指定憑證檔案相對於您在屬性中指定的目錄的位 `config.resourcesDirectory` 置。

**Flash Media Rights Management Server** —— 檔 `flashaccess-refimpl.properties` 案也包含數個與封裝內容相關的屬性。 這些屬性僅用於Flash Media Rights Management Server 1.x中繼資料轉換。 修改此屬性檔案中的值後，如果更改生效，請重新啟動許可證伺服器。
