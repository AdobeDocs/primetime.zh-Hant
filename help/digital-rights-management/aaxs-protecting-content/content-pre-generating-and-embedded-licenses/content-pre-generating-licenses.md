---
title: 預生成許可證
description: 預生成許可證
copied-description: true
exl-id: 2be8674c-736f-4ed3-b952-f661bf3ff48f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 預生成許可證{#pre-generating-licenses}

要預生成許可證，請使用 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 獲取 `LicenseFactory`。 必須指定許可證伺服器憑據才能對此工廠生成的許可證進行簽名。 此類支援生成葉許可證（無許可證連結）和葉和根許可證(具有 [增強的許可證連結](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md)。

生成葉許可證時，必須使用 `initContentInfo()`。 如果元資料包含多個策略，或者您希望使用元資料中未包含的策略，請使用 `setSelectedPolicy()` 指定用於生成許可證的策略。 如果使用策略更新清單跟蹤策略的更新，則可以在使用初始化元資料之前將策略更新清單提供給許可證工廠 `setPolicyUpdateList()`。

當生成根許可證時，可以如上所述指定內容元資料。 或者，可以使用策略( `setSelectedPolicy()`)和許可證伺服器URL( `setLicenseServerURL()`)而不是元資料。

>[!NOTE]
>
>即使沒有Adobe訪問許可證伺服器，客戶端也可以從中請求許可證，也需要許可證伺服器URL。 在這種情況下，許可證伺服器URL應指定標識許可證頒發者的URL。

如果策略使用增強的許可證連結，則必須指定許可證伺服器憑據才能解密策略中的根加密密鑰( `setRootKeyRetrievalInfo()`)。

如果策略需要域綁定許可證，請使用 `setDomainCAs()` 指定許可證伺服器將從中接受域令牌的域發行者。 必須提供一個或多個域CA證書才能驗證許可證收件人。

如果策略要求iOS設備的遠程密鑰傳遞，則必須使用 `setKeyServerCertificate()`，除非生成連結葉。

要生成許可證，請調用 `generateLicense()` 並指定許可證類型（葉或根）和一個或多個收件人證書。 接收者證書將是電腦證書或域證書，具體取決於策略中指定的要求。 如果要生成鏈式葉，則不需要收件人。 在生成許可證後，可以覆蓋策略中指定的使用規則。 最後，調用 `signLicense()` 簽署許可證並獲取 `PreGeneratedLicense`。 現在可以將許可證保存到檔案(使用 `getBytes()` 檢索序列化許可證)或嵌入加密內容。 看， [嵌入許可證](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md)。

有關演示預生成許可證的示例代碼，請參見 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 在「參考實現」命令行工具「示例」目錄中。
