---
description: 如果使用Adobe PrimetimeDRM Professional，則可以預生成許可證並將許可證嵌入到內容中。 此功能可以與增強的許可證連結相組合，使得葉許可證被預生成並嵌入到內容中，並且客戶機可以從許可證伺服器請求根許可證（綁定到電腦或域）。 或者，客戶端應用程式可以實現一個工作流，其中設備預註冊到伺服器，伺服器預生成綁定到該設備的許可，並且客戶端從簡單的HTTP Web伺服器檢索其許可。
title: 預生成許可證
exl-id: 6ced7dde-b4bb-470d-bdae-3042f5577b67
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 預生成許可證 {#pre-generating-licenses}

如果使用Adobe PrimetimeDRM Professional，則可以預生成許可證並將許可證嵌入到內容中。 此功能可以與增強的許可證連結相組合，使得葉許可證被預生成並嵌入到內容中，並且客戶機可以從許可證伺服器請求根許可證（綁定到電腦或域）。 或者，客戶端應用程式可以實現一個工作流，其中設備預註冊到伺服器，伺服器預生成綁定到該設備的許可，並且客戶端從簡單的HTTP Web伺服器檢索其許可。

如果要預生成許可證，必須使用 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 獲取 `LicenseFactory`。 必須指定許可證伺服器憑據才能對此工廠生成的許可證進行簽名。 此類支援生成葉許可證（無許可證連結）和葉和根許可證(具有 [增強的許可證連結](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md)。

生成葉許可證時，必須指定應用的內容元資料 `initContentInfo()`。 如果元資料包括多個DRM策略，或者如果您想使用元資料中未包括的DRM策略，則必須使用 `setSelectedPolicy()` 指定DRM策略以生成許可證。 如果使用DRM策略更新清單跟蹤對DRM策略的更新，則可以先將DRM策略更新清單提供給許可證工廠，然後使用初始化元資料 `setPolicyUpdateList()`。

生成根許可證時，必須按上述說明指定內容元資料。 或者，可以通過應用DRM策略( `setSelectedPolicy()`)和許可證伺服器URL( `setLicenseServerURL()`)而不是元資料。

>[!NOTE]
>
>即使沒有客戶端可以從中請求許可證的Adobe PrimetimeDRM許可證伺服器，也需要許可證伺服器URL。 在這種情況下，許可證伺服器URL應指定標識許可證頒發者的URL。

如果DRM策略使用增強的許可證連結，則必須指定許可證伺服器憑據以解密DRM策略中的根加密密鑰( `setRootKeyRetrievalInfo()`)。

如果DRM策略需要域綁定許可證，則必須使用 `setDomainCAs()` 指定許可證伺服器從中接受域令牌的域發行者。 必須提供一個或多個域CA證書才能驗證許可證收件人。

如果DRM策略要求iOS設備的遠程密鑰傳遞，則必須通過應用來提供密鑰伺服器證書 `setKeyServerCertificate()` 除非生成連結葉。

如果要生成許可證，必須調用 `generateLicense()` 並指定許可證類型（葉或根）和一個或多個收件人證書。 收件者證書表示電腦證書或域證書，具體取決於在DRM策略中指定的要求。 如果生成鏈式葉，則不需要收件人。 在生成許可證後，可以覆蓋在DRM策略中指定的使用規則。 最後，你需要調用 `signLicense()` 簽署許可證並獲取 `PreGeneratedLicense`。 現在可以保存許可證(使用 `getBytes()` 檢索序列化許可證或嵌入加密內容。

請參閱 [嵌入許可證](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md)。

請參閱 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 在「參考實現」命令行工具「示例」目錄中，獲取有關如何演示預生成的許可證的示例代碼。
