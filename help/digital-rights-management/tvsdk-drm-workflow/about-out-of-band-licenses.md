---
title: 帶外授權概觀
description: 帶外授權概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# 帶外許可證{#out-of-band-licenses}

此外，也可使用`storeVoucher()`方法，將授權儲存在磁碟和記憶體中，以帶外方式（不需聯絡Primetime DRM授權伺服器）取得授權。

若要在Primetime中播放加密的視訊，個別執行階段必須取得該視訊的授權。 授權包含視訊的解密金鑰，並由客戶所部署的Primetime DRM授權伺服器產生。

運行時通常通過向視頻的DRM元資料（`DRMContentData`類）中指示的Primetime DRM許可伺服器發送許可請求來獲得此許可。 應用程式可以呼叫`DRMManager.loadVoucher()`方法來觸發此授權要求。

`DRMManager.storeVoucher()` 允許應用程式傳送其取得的帶外授權。然後，執行階段可略過授權要求程式，並使用轉送的授權來播放加密的視訊。 授權仍需由Primetime DRM授權伺服器產生，才能在帶外取得。 不過，您可以選擇在任何HTTP伺服器上代管授權，而非Primetime DRM授權伺服器。

`DRMManager.storeVoucher()` 也用於支援多種裝置間的授權共用。在Primetime DRM 3.0之後，此功能稱為「裝置網域支援」。 如果您的部署支援此使用案例，則可以使用`DRMManager.addToDeviceGroup()`方法將多台電腦註冊到設備組。 如果某台機器擁有特定內容的有效網域界限授權，則應用程式可使用`DRMVoucher.toByteArray()`方法擷取序號的授權，而您也可以在其他電腦上使用`DRMManager.storeVoucher()`方法匯入授權。

## 關於設備註冊{#about-device-registration}

所有Primetime DRM授權在建立時都必須系結至終端實體。 綁定是僅允許特定實體使用許可證的加密過程。 這是防止任何任意設備都可以使用的「浮動許可證」所必需的。 對於Primetime DRM，若要「預先產生」授權，這表示這些預先產生的授權的「目標」必須事先知道。 Primetime DRM將此稱為「裝置註冊」。

## 註冊設備{#register-a-device}

假設您已執行下列工作：

* 您已設定Primetime DRM Server SDK。
* 您已設定HTTP伺服器，以發行預先產生的授權。
* 您已建立Primetime應用程式來檢視受保護的內容。

 裝置註冊階段包含下列動作：

1. 應用程式會建立隨機產生的ID。
1. 應用程式調用`DRMManager.authenticate()`方法。 應用程式必須在驗證要求中包含隨機產生的ID。 例如，在使用者名稱欄位中加入ID。
1. 步驟2中提及的動作將導致Primetime DRM傳送驗證要求至客戶的伺服器。 此請求包含裝置憑證：
   1. 伺服器從請求中提取設備證書和生成的ID並儲存。
   1. 客戶子系統預生成此設備證書的許可證，儲存這些許可證並以使它們與生成的ID相關聯的方式授予對它們的訪問權。.
1. 伺服器會以「成功」訊息回應要求。
1. 應用程式儲存產生的ID。

在裝置註冊後，應用程式會以先前方案中使用裝置ID的相同方式使用產生的ID:
1. 應用程式會嘗試找出產生的ID。
1. 如果找到產生的ID，應用程式會在下載預先產生的授權時使用產生的ID。 應用程式會將授權傳送至Primetime DRM用戶端，以使用`DRMManager.storeVoucher()`方法。.
1. 如果找不到產生的ID，應用程式將會執行裝置註冊程式。

## DRM工廠重置{#drm-factory-reset}

當裝置的使用者叫用DRM工廠重設選項時，裝置憑證將會被清除。 若要繼續播放受保護的內容，應用程式必須再次執行裝置註冊程式。 如果應用程式傳送過期的預先產生授權，Primetime DRM用戶端會拒絕，因為授權已針對舊版裝置ID加密。

* FlashAPI:[DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) -（僅能響應某些不可恢復的DRM錯誤代碼而調用。）
* iOS API:[DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* Android API:[DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))