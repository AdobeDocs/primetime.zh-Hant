---
title: 頻外授權概述
description: 頻外授權概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 頻外授權 {#out-of-band-licenses}

也可以使用將授權儲存在磁碟和記憶體中，在頻外（不連絡Primetime DRM授權伺服器）取得授權 `storeVoucher()` 方法。

若要在Primetime中播放加密的視訊，個別執行階段需要取得該視訊的授權。 授權包含視訊的解密金鑰，由客戶已部署的Primetime DRM授權伺服器產生。

執行階段通常會透過傳送授權請求給視訊的DRM中繼資料( `DRMContentData` 類別)。 應用程式可以呼叫 `DRMManager.loadVoucher()` 方法。

`DRMManager.storeVoucher()` 可讓應用程式傳送其已在頻外取得的授權。 然後，執行階段可以略過授權請求程式，並使用轉送的授權播放加密的視訊。 授權仍需由Primetime DRM授權伺服器產生，才能在頻外取得。 不過，您可以選擇在任何HTTP伺服器上裝載授權，而不是Primetime DRM授權伺服器。

`DRMManager.storeVoucher()` 也用於支援多部裝置之間的授權共用。 在Primetime DRM 3.0之後，此功能稱為「裝置網域支援」。 如果您的部署支援此使用案例，您可以使用將多部機器註冊到裝置群組 `DRMManager.addToDeviceGroup()` 方法。 如果機器對特定內容具有有效的網域繫結授權，則應用程式可以使用 `DRMVoucher.toByteArray()` 方法，而您可在其他電腦上，使用 `DRMManager.storeVoucher()` 方法。

## 關於裝置註冊 {#about-device-registration}

所有Primetime DRM許可證在建立時都必須繫結到終端圖元。 繫結是僅允許特定實體能夠使用授權的密碼編譯程式。 這是必要的，以防止任何任意裝置都可以使用的「浮動授權」。 對於Primetime DRM「預先產生」授權，這表示必須事先知道這些預先產生授權的「目標」。 Primetime DRM將此稱為「裝置註冊」。

## 註冊裝置 {#register-a-device}

假設您已執行下列工作：

* 您已設定Primetime DRM Server SDK。
* 您已設定HTTP伺服器以核發預先產生的授權。
* 您已建立Primetime應用程式來檢視受保護的內容。

 裝置註冊階段包含下列動作：

1. 應用程式會建立隨機產生的ID。
1. 應用程式會叫用 `DRMManager.authenticate()` 方法。 應用程式必須在驗證請求中包含隨機產生的ID。 例如，請在使用者名稱欄位中加入ID。
1. 步驟2中提到的動作會導致Primetime DRM傳送驗證請求給客戶的伺服器。 此請求包含裝置憑證：
   1. 伺服器會從要求中擷取裝置憑證及產生的ID，然後加以儲存。
   1. 客戶子系統預先產生此裝置憑證的授權、儲存這些授權，並以將其與產生的ID建立關聯的方式授予對這些授權的存取權。.
1. 伺服器以「success」訊息回應要求。
1. 應用程式會儲存產生的ID。

在裝置註冊之後，應用程式會使用產生的ID，其使用方式與先前配置中使用的裝置ID相同：
1. 應用程式將嘗試找出產生的ID。
1. 如果找到產生的ID，應用程式將在下載預先產生的授權時使用產生的ID。 應用程式會使用將授權傳送至Primetime DRM使用者端以供使用 `DRMManager.storeVoucher()` 方法。.
1. 如果找不到產生的ID，應用程式將進行裝置註冊程式。

## DRM原廠重設 {#drm-factory-reset}

當裝置的使用者叫用DRM原廠重設選項時，將會清除裝置憑證。 若要繼續播放受保護的內容，應用程式必須再次進行裝置註冊程式。 如果應用程式傳送過時的預先產生授權，Primetime DRM使用者端會拒絕它，因為授權是以舊裝置ID加密。

* Flash API： [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - （只能呼叫來回應某些無法復原的DRM錯誤碼。）
* iOS API： [DRManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* Android API： [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))
