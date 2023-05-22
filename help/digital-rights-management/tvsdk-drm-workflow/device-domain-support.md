---
description: 通常，所有黃金時段DRM許可證在建立時都綁定到唯一設備。 此綁定防止用戶在不經授權的情況下跨不同設備共用許可證。 除了每設備綁定外，Mighine DRM還提供了將許可證綁定到設備域或設備組的能力。
title: 使用域支援播放加密內容
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 設備域支援 {#device-domain-support}

通常，所有黃金時段DRM許可證在建立時都綁定到唯一設備。 此綁定防止用戶在不經授權的情況下跨不同設備共用許可證。 除了每設備綁定外，Mighine DRM還提供了將許可證綁定到設備域或設備組的能力。

如果內容元資料指定需要設備域註冊，則應用程式可以調用API以加入設備組。 此操作將觸發要發送到域伺服器的域註冊請求。 一旦向設備組發放許可證，就可以導出該許可證並與已加入設備組的其他設備共用。

然後，在中使用設備組資訊 `DRMContentData` `VoucherAccessInfo` 對象，然後該對象將用於顯示成功檢索和使用許可證所需的資訊。

## 使用域支援播放加密內容 {#play-encrypted-content-using-domain-support}

要使用Mighine DRM播放加密內容，請執行以下步驟：

1. 使用 `VoucherAccessInfo.deviceGroup`，檢查是否需要註冊設備組。
1. 如果需要身份驗證：
   1. 使用 `DeviceGroupInfo.authenticationMethod` 屬性，查看是否需要驗證。
   1. 如果需要驗證，請執行以下步驟之一來驗證用戶：

      * 獲取用戶的用戶名和密碼並調用 `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`。
      * 獲取快取/預生成的驗證令牌並調用 `DRMManager.setAuthenticationToken()`。
   1. 調用 `DRMManager.addToDeviceGroup()`
1. 通過執行以下任務之一獲取內容許可證：
   1. 使用 `DRMManager.loadVoucher()` 的雙曲餘切值。
   1. 從在同一設備組中註冊的不同設備獲取許可證，並將許可證提供給 `DRMManager` 通過 `DRMManager.storeVoucher()` 的雙曲餘切值。
1. 使用 `Primetime.play()` 的雙曲餘切值。
要導出內容的許可證，任何設備都可以使用 `DRMVoucher.toByteArray()` 從黃金時段DRM許可伺服器獲取許可證後的方法。 內容提供者通常限制設備組中的設備數量。 如果達到限制，則可能需要調用 `DRMManager.removeFromDeviceGroup()` 在註冊當前設備之前對未使用設備執行方法。
