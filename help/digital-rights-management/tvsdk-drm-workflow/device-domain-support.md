---
description: 通常，所有Primetime DRM授權在建立時都會系結至獨特的裝置。 此系結可防止使用者在未取得授權的情況下，在不同裝置間共用授權。 除了依裝置進行系結外，Primetime DRM還提供將授權系結至裝置網域或裝置群組的能力。
seo-description: 通常，所有Primetime DRM授權在建立時都會系結至獨特的裝置。 此系結可防止使用者在未取得授權的情況下，在不同裝置間共用授權。 除了依裝置進行系結外，Primetime DRM還提供將授權系結至裝置網域或裝置群組的能力。
seo-title: 使用網域支援播放加密內容
title: 使用網域支援播放加密內容
uuid: 8854cc0f-9bfc-4833-82d7-a3f46ac88e06
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 裝置網域支援 {#device-domain-support}

通常，所有Primetime DRM授權在建立時都會系結至獨特的裝置。 此系結可防止使用者在未取得授權的情況下，在不同裝置間共用授權。 除了依裝置進行系結外，Primetime DRM還提供將授權系結至裝置網域或裝置群組的能力。

如果內容中繼資料指定需要裝置網域註冊，應用程式就可以叫用API來加入裝置群組。 此操作會觸發要發送到域伺服器的域註冊請求。 一旦授權發放至裝置群組後，即可匯出授權並與已加入裝置群組的其他裝置共用。

然後，設備組資訊將用於對 `DRMContentData``VoucherAccessInfo` 像中，該對象隨後將用於顯示成功檢索和使用許可證所需的資訊。

## 使用網域支援播放加密內容 {#play-encrypted-content-using-domain-support}

若要使用Primetime DRM播放加密內容，請執行下列步驟：

1. 使用 `VoucherAccessInfo.deviceGroup`時，檢查是否需要註冊設備組。
1. 如果需要驗證：
   1. 使用屬 `DeviceGroupInfo.authenticationMethod` 性找出是否需要驗證。
   1. 如果需要驗證，請執行下列步驟之一來驗證用戶：

      * 取得使用者的使用者名稱和密碼並叫用 `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`。
      * 取得快取／預先產生的驗證Token並叫用 `DRMManager.setAuthenticationToken()`。
   1. 叫用 `DRMManager.addToDeviceGroup()`
1. 執行下列任務之一，以取得內容授權：
   1. 使用方 `DRMManager.loadVoucher()` 法。
   1. 從相同裝置群組中註冊的不同裝置取得授權，並透過方法提供 ` DRMManager` 授權 `DRMManager.storeVoucher()` 給。
1. 使用方法播放加密的 `Primetime.play()` 內容。
為了匯出內容的授權，任何裝置在從Primetime DRM授權伺服器取得授權後，都可使用 `DRMVoucher.toByteArray()` 方法提供授權的原始位元組。 內容提供者通常會限制裝置群組中的裝置數目。 如果達到限制，您可能需要在未使用的裝 `DRMManager.removeFromDeviceGroup()` 置上呼叫方法，才能註冊目前的裝置。