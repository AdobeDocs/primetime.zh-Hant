---
description: 通常，所有Primetime DRM授權在建立時都會系結至獨特的裝置。 此系結可防止使用者在未取得授權的情況下，跨不同裝置共用授權。 除了依裝置進行系結外，Primetime DRM還提供將授權系結至裝置網域或裝置群組的能力。
title: 使用網域支援播放加密內容
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# 設備域支援{#device-domain-support}

通常，所有Primetime DRM授權在建立時都會系結至獨特的裝置。 此系結可防止使用者在未取得授權的情況下，跨不同裝置共用授權。 除了依裝置進行系結外，Primetime DRM還提供將授權系結至裝置網域或裝置群組的能力。

如果內容中繼資料指定需要裝置網域註冊，應用程式就可以叫用API來加入裝置群組。 此操作會觸發要發送到域伺服器的域註冊請求。 一旦授權發放至裝置群組後，即可匯出授權並與已加入裝置群組的其他裝置共用。

然後，設備組資訊將用於`DRMContentData` `VoucherAccessInfo`對象中，該對象隨後將用於顯示成功檢索和使用許可證所需的資訊。

## 使用網域支援{#play-encrypted-content-using-domain-support}播放加密內容

若要使用Primetime DRM播放加密內容，請執行下列步驟：

1. 使用`VoucherAccessInfo.deviceGroup`，檢查是否需要註冊設備組。
1. 如果需要驗證：
   1. 使用`DeviceGroupInfo.authenticationMethod`屬性瞭解是否需要驗證。
   1. 如果需要驗證，請執行下列步驟之一來驗證用戶：

      * 獲取用戶的用戶名和密碼並調用`DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`。
      * 取得快取／預先產生的驗證Token並叫用`DRMManager.setAuthenticationToken()`。
   1. 叫用`DRMManager.addToDeviceGroup()`
1. 執行下列任務之一，以取得內容授權：
   1. 使用`DRMManager.loadVoucher()`方法。
   1. 從相同裝置群組中註冊的不同裝置取得授權，並透過`DRMManager.storeVoucher()`方法將授權提供給` DRMManager`。
1. 使用`Primetime.play()`方法播放加密內容。
若要匯出內容的授權，任何裝置在從Primetime DRM授權伺服器取得授權後，都可使用`DRMVoucher.toByteArray()`方法提供授權的原始位元組。 內容提供者通常會限制裝置群組中的裝置數目。 如果達到此限制，您可能需要在註冊當前設備之前，在未使用的設備上調用`DRMManager.removeFromDeviceGroup()`方法。