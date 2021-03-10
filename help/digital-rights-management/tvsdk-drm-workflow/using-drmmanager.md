---
title: 使用DRMManager類概述
description: 使用DRMManager類概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# 使用DRMManager類{#using-the-drmmanager-class}

使用`DRMManager`類別來管理應用程式中的授權和Primetime DRM授權伺服器作業。

**授權管理**

每當裝置播放受保護的內容時，執行時期就會取得並快取檢視內容所需的授權。 如果應用程式將內容儲存在本機，而授權允許離線播放，使用者就可以在沒有網路連線的情況下檢視應用程式中的內容。 使用`DRMManager`，您可以預快取許可證。 應用程式不需要取得檢視內容所需的授權。 例如，您的應用程式可下載媒體檔案，然後在使用者仍線上時取得授權。

若要預先載入授權，請使用`DRMContentData`物件。 `DRMContentData`物件包含Primetime DRM授權伺服器的URL，可提供授權並說明是否需要使用者驗證。 使用此資訊，您可以調用`DRMManager` `loadVoucher()`方法來獲取和快取許可證。 *預載離線播放授權*&#x200B;中會更詳細地說明預載授權的工作流程。

**會話管理**

您也可以使用`DRMManager`來向Primetime DRM授權伺服器驗證使用者，並管理持久性工作階段。 呼叫`DRMManager` `authenticate()`方法以建立與Primetime DRM授權伺服器的作業。 驗證成功完成後，`DRMManager`將調度`DRMAuthenticationCompleteEvent`對象。 此物件包含作業Token。 您可以儲存此Token以建立未來的工作階段，如此使用者就不需要提供其帳戶憑證。 將Token傳遞至`setAuthenticationToken()`方法，以建立新的已驗證作業。 （產生代號的伺服器設定會決定代號過期時間和其他屬性）。

## 處理DRMStatus事件{#handling-drmstatus-events}

`DRMManager`在對`loadVoucher()`方法的調用成功完成後調度`DRMStatusEvent`對象。 如果獲得許可證，則事件對象的detail屬性具有以下值：`DRM.voucherObtained`，而憑證屬性包含`DRMVoucher`物件。 如果未取得授權，則detail屬性仍具有下列值：`DRM.voucherObtained`;但是，憑單屬性為null。 例如，如果您使用`localOnly`的`LoadVoucherSetting`且沒有本機快取的授權，則無法取得授權。 如果`loadVoucher()`呼叫未成功完成，可能是由於驗證或通信錯誤，則`DRMManager`會改為調度`DRMErrorEvent`或`DRMAuthenticationErrorEvent`對象。

## 處理DRMAuthenticationComplete事件{#handling-drmauthenticationcomplete-events}

當用戶通過對`authenticate()`方法的調用成功驗證時，`DRMManager`調度`DRMAuthenticationCompleteEvent`對象。 `DRMAuthenticationCompleteEvent`物件包含可重複使用的Token，可用來跨應用程式作業持續使用者驗證。 將此Token傳遞至`DRMManager` `setAuthenticationToken()`方法以重新建立工作階段。 (Token製作程式會設定Token屬性，例如過期。 Adobe不提供檢查Token屬性的API。)

## 處理DRMAuthenticationError事件{#handling-drmauthenticationerror-events}

當無法通過對`authenticate()`或`setAuthenticationToken()`方法的調用成功驗證用戶時，`DRMManager`調度`DRMAuthenticationErrorEvent`對象。