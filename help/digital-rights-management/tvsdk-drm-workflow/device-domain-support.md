---
description: 通常，所有Primetime DRM授權在建立時都會系結至獨特裝置。 此捆綁可防止用戶在不經授權的情況下跨不同設備共用許可證。 除了每個裝置系結外，Primetime DRM還提供將授權系結至裝置網域或裝置群組的功能。
title: 使用網域支援播放加密內容
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 設備域支援{#device-domain-support}

通常，所有Primetime DRM授權在建立時都會系結至獨特裝置。 此捆綁可防止用戶在不經授權的情況下跨不同設備共用許可證。 除了每個裝置系結外，Primetime DRM還提供將授權系結至裝置網域或裝置群組的功能。

如果內容元資料指定需要設備域註冊，則應用程式可以調用API以加入設備組。 此操作將觸發域註冊請求被發送到域伺服器。 在將許可證頒發給設備組後，可以導出該許可證並與已加入設備組的其他設備共用。

然後，設備組資訊將用於`DRMContentData` `VoucherAccessInfo`對象中，該對象將用於提供成功檢索和使用許可證所需的資訊。

## 使用域支援{#play-encrypted-content-using-domain-support}播放加密內容

若要使用Primetime DRM播放加密內容，請執行下列步驟：

1. 使用`VoucherAccessInfo.deviceGroup`檢查是否需要設備組註冊。
1. 如果需要驗證：
   1. 使用`DeviceGroupInfo.authenticationMethod`屬性查明是否需要身份驗證。
   1. 如果需要身份驗證，請執行以下步驟之一來驗證用戶：

      * 獲取用戶的用戶名和密碼並調用`DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`。
      * 獲取快取/預生成的驗證令牌並調用`DRMManager.setAuthenticationToken()`。
   1. 調用`DRMManager.addToDeviceGroup()`
1. 執行下列任務之一，以取得內容的授權：
   1. 使用`DRMManager.loadVoucher()`方法。
   1. 從在同一設備組中註冊的不同設備獲取許可證，並通過`DRMManager.storeVoucher()`方法向`DRMManager`提供許可證。
1. 使用`Primetime.play()`方法播放加密的內容。
要導出內容的許可證，任何設備都可以在從Primetime DRM許可證伺服器獲取許可證後使用`DRMVoucher.toByteArray()`方法提供許可證的原始位元組。 內容提供者通常會限制裝置群組中的裝置數量。 如果達到限制，則在註冊當前設備之前，可能需要在未使用的設備上調用`DRMManager.removeFromDeviceGroup()`方法。
