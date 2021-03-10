---
title: 許可證伺服器屬性檔案
description: 許可證伺服器屬性檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# 許可證伺服器屬性檔案{#license-server-properties-file}

許可證伺服器引用在[!DNL flashaccess-refimpl.properties]檔案中設定的屬性。 您可以直接參考該檔案，以取得特定值的詳細資訊，以及每個屬性的使用資訊。 在參考實施的[!DNL resources]目錄(`([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`)中提供了完全功能示例。

**憑據** -屬性檔案包括向您發出Adobe的憑據的位置設定。您可以在[!DNL .pfx]檔案中指定這些憑據，並使用口令，或為儲存在HSM上的憑據提供別名和口令。 您至少需要配置與傳輸憑證和許可證伺服器憑證相關的屬性。 指定憑證檔案相對於您在`config.resourcesDirectory`屬性中指定的目錄的位置。

**Flash媒體Rights Management伺服器** -該文 `flashaccess-refimpl.properties` 件還包括與打包內容相關的多個屬性。這些屬性僅用於Flash媒體Rights Management伺服器1.x元資料轉換。 修改此屬性檔案中的值後，如果更改生效，請重新啟動許可證伺服器。
