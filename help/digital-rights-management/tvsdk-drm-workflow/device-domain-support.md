---
description: 通常，所有Primetime DRM授權在建立時都會繫結到唯一裝置。 此繫結可防止使用者未經授權而跨不同裝置共用授權。 除了每個裝置的繫結外，Primetime DRM還提供將授權繫結到裝置網域或裝置群組的功能。
title: 使用網域支援播放加密的內容
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 裝置網域支援 {#device-domain-support}

通常，所有Primetime DRM授權在建立時都會繫結到唯一裝置。 此繫結可防止使用者未經授權而跨不同裝置共用授權。 除了每個裝置的繫結外，Primetime DRM還提供將授權繫結到裝置網域或裝置群組的功能。

如果內容中繼資料指定需要裝置網域註冊，應用程式可以叫用API來加入裝置群組。 這個動作會觸發要傳送至網域伺服器的網域註冊要求。 將授權核發至裝置群組後，即可匯出授權並與已加入裝置群組的其他裝置共用。

然後，裝置群組資訊會用於 `DRMContentData` `VoucherAccessInfo` 物件，然後用於呈現成功擷取和使用授權所需的資訊。

## 使用網域支援播放加密的內容 {#play-encrypted-content-using-domain-support}

若要使用Primetime DRM播放加密的內容，請執行下列步驟：

1. 使用 `VoucherAccessInfo.deviceGroup`，檢查是否需要裝置群組註冊。
1. 如果需要驗證：
   1. 使用 `DeviceGroupInfo.authenticationMethod` 屬性，瞭解是否需要驗證。
   1. 如果需要驗證，請執行以下步驟之一來驗證使用者：

      * 取得使用者的使用者名稱和密碼並叫用 `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * 取得快取/預先產生的驗證權杖並叫用 `DRMManager.setAuthenticationToken()`.
   1. 叫用 `DRMManager.addToDeviceGroup()`
1. 執行下列其中一項工作，以取得內容的授權：
   1. 使用 `DRMManager.loadVoucher()` 方法。
   1. 從同一裝置群組中註冊的不同裝置取得授權，並將授權提供給 `DRMManager` 透過 `DRMManager.storeVoucher()` 方法。
1. 使用播放加密的內容 `Primetime.play()` 方法。
若要匯出內容的授權，任何裝置都可使用 `DRMVoucher.toByteArray()` 從Primetime DRM授權伺服器取得授權後的方法。 內容提供者通常會限制裝置群組中的裝置數量。 如果達到限制，您可能需要呼叫 `DRMManager.removeFromDeviceGroup()` 註冊目前裝置之前，在未使用裝置上執行的方法。
