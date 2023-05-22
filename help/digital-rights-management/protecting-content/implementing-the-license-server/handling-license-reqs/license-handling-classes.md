---
title: 概述
description: 概述
copied-description: true
exl-id: 267188d0-83f8-42dc-88e3-78b52945cb6c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 概述 {#overview}

為了獲得許可證，客戶端從嵌入在打包內容中的元資料形成請求，然後將該請求提交到許可證伺服器。 許可證伺服器使用從內容元資料中提取的資訊來生成許可證。

如果客戶端和伺服器都支援協定版本5，則請求URL為「元資料中的許可證伺服器URL」 + &quot; [!DNL /flashaccess/license/v4]。 如果協定版本3是客戶端或伺服器支援的最大版本，則Mighine DRM客戶端隨後將驗證請求發送到「元資料中的許可證伺服器URL」 + &quot; [!DNL /flashaccess/license/v3]。 否則，將驗證請求發送到「元資料中的許可證伺服器URL」 + &quot; [!DNL /flashaccess/license/v1]&quot;

設備可以具有用於相同內容的多個許可證（相同的許可證ID），但只能具有用於特定許可證ID和DRM策略ID的一個許可證。 如果它收到具有重複的LicenseID/PolicyID的許可證，則僅當新許可證的頒發日期晚於現有許可證的頒發日期時，新許可證才會替換舊許可證。 此邏輯用於處理嵌入到內容中的許可證。 因此，建議不要在內容塊中嵌入多個具有相同DRM策略ID的許可證。 同樣的邏輯適用於通過 `DRMManager.storeVoucher()` ActionScript3 API;如果客戶端已經擁有具有稍後發放日期的許可證，則可忽略提供的許可證。

## 許可證請求處理類 {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`  — 這是許可證請求處理程式類。 它讀取並解析許可證請求。 其 `getRequests()` 方法返回清單 `LicenseRequestMessage` 對象。
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`  — 這是請求消息類。 調用方應迭代 `LicenseRequestMessage` 返回的清單 `getRequests()`，並為每個請求生成許可證或設定錯誤代碼。 呼叫 `LicenseRequestMessage.getContentInfo()` 從內容元資料（包括內容ID、許可ID和DRM策略）中獲取資訊。

許可證和錯誤在 `LicenseHandler.close()` 調用方法。

查看 [DRM伺服器API參考文檔](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) 的雙曲餘切值。
