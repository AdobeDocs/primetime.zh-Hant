---
seo-title: 概觀
title: 概觀
uuid: 2bbf0aa1-df35-429d-84df-db357fa53e47
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# 概述{#overview}

為取得授權，用戶端會從內嵌在封裝內容中的中繼資料提出要求，然後將該要求提交至授權伺服器。 許可伺服器使用從內容元資料提取的資訊來生成許可。

如果客戶端和伺服器都支援第5版協定，請求URL為「元資料中的許可證伺服器URL」 + &quot; [!DNL /flashaccess/license/v4]&quot;。 如果協定版本3是客戶端或伺服器所支援的最大值，則Primetime DRM客戶端會向「License Server URL in metadata」 + &quot; [!DNL /flashaccess/license/v3]&quot;發送驗證請求。 否則，驗證請求會傳送至「中繼資料中的授權伺服器URL」+「 [!DNL /flashaccess/license/v1]」

裝置可針對相同內容（相同的授權ID）擁有多份授權，但特定授權ID和DRM政策ID只能有一份授權。 如果收到具有重複LicenseID/PolicyID的授權，則新授權僅在新授權的發行日期晚於現有授權的發行日期時，才會取代舊授權。 此邏輯用於處理內嵌在內容中的授權。 因此，建議不要在內容區塊中嵌入多個具有相同DRM原則ID的授權。 同樣的邏輯也適用於透過`DRMManager.storeVoucher()` ActionScript3 API傳遞給用戶端的授權；如果用戶端已擁有授權，且日後發行日期已過，則可能會忽略所提供的授權。

## 授權要求處理類別{#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` -這是授權要求處理常式類別。它會讀取並解析授權要求。 其`getRequests()`方法返回`LicenseRequestMessage`對象的清單。
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` -這是請求消息類。呼叫者應重複`getRequests()`傳回的`LicenseRequestMessage`清單，並針對每個請求產生授權或設定錯誤碼。 呼叫`LicenseRequestMessage.getContentInfo()`以取得從內容中繼資料擷取的資訊，包括內容ID、授權ID和DRM原則。

當呼叫`LicenseHandler.close()`方法時，會同時傳送授權和錯誤。

如需詳細資訊，請參閱[DRM伺服器API參考檔案](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html)。
