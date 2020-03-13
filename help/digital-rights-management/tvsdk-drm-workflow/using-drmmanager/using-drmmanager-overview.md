---
seo-title: 使用DRMManager類概述
title: 使用DRMManager類概述
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 使用DRMManager類 {#using-the-drmmanager-class}

使用此類 `DRMManager` 別來管理應用程式中的授權和Primetime DRM授權伺服器作業。

**授權管理**

每當裝置播放受保護的內容時，執行時期就會取得並快取檢視內容所需的授權。 如果應用程式將內容儲存在本機，而授權允許離線播放，使用者就可以在沒有網路連線的情況下檢視應用程式中的內容。 使用 `DRMManager`，您可以預快取許可證。 應用程式不需要取得檢視內容所需的授權。 例如，您的應用程式可下載媒體檔案，然後在使用者仍線上時取得授權。

若要預先載入授權，請使用 `DRMContentData` 物件。 此物 `DRMContentData` 件包含Primetime DRM授權伺服器的URL，可提供授權並說明是否需要使用者驗證。 有了這些資訊，您可以呼叫方 `DRMManager` 法以取得 `loadVoucher()` 和快取授權。 預載授權的工作流程在離線播放的預載 *授權中有更詳細的說明*。

**會話管理**

您也可以使用來 `DRMManager` 向Primetime DRM授權伺服器驗證使用者，並管理持久性工作階段。 呼叫方 `DRMManager` 法以建 `authenticate()` 立與Primetime DRM授權伺服器的作業。 驗證成功完成後，將調 `DRMManager` 度對 `DRMAuthenticationCompleteEvent` 像。 此物件包含作業Token。 您可以儲存此Token以建立未來的工作階段，如此使用者就不需要提供其帳戶憑證。 將Token傳遞至方 `setAuthenticationToken()` 法，以建立新的驗證作業。 （產生代號的伺服器設定會決定代號過期時間和其他屬性）。

## 處理DRMStatus事件 {#handling-drmstatus-events}

在對 `DRMManager` 方法 `DRMStatusEvent` 的調用成功完成後，調 `loadVoucher()` 度對象。 如果獲得許可證，則事件對象的detail屬性具有以下值：而 `DRM.voucherObtained`憑證屬性則包含物 `DRMVoucher` 件。 如果未取得授權，則detail屬性仍具有下列值： `DRM.voucherObtained`;但是，憑單屬性為null。 例如，如果您使用的是，且沒有本機快取的 `LoadVoucherSetting` 授 `localOnly` 權，則無法取得授權。 如果 `loadVoucher()` 呼叫未成功完成（可能是由於驗證或通訊錯誤），則派 `DRMManager` 單或 `DRMErrorEvent` 物 `DRMAuthenticationErrorEvent` 件。

## 處理DRMAuthenticationComplete事件{#handling-drmauthenticationcomplete-events}

當用 `DRMManager` 戶通過 `DRMAuthenticationCompleteEvent` 對方法的調用成功地驗證時，調度對象 `authenticate()` 。 物 `DRMAuthenticationCompleteEvent` 件包含可重複使用的Token，可用來跨應用程式作業保存使用者驗證。 將此Token傳 `DRMManager` 遞至 `setAuthenticationToken()` 方法以重新建立工作階段。 (Token製作程式會設定Token屬性，例如過期。 Adobe不提供檢查Token屬性的API。)

## 處理DRMAuthenticationError事件{#handling-drmauthenticationerror-events}

當用 `DRMManager` 戶無 `DRMAuthenticationErrorEvent` 法通過對或方法的調用成功驗證時，調度對 `authenticate()` 像 `setAuthenticationToken()` 。