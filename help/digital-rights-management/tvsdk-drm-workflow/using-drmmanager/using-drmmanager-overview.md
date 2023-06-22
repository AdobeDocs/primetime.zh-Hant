---
title: 使用DRMManager類別概觀
description: 使用DRMManager類別概觀
copied-description: true
exl-id: 941a69fb-3085-45d6-9176-08ebb93cada4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 使用DRMManager類別 {#using-the-drmmanager-class}

使用 `DRMManager` 類別以管理應用程式中的授權和Primetime DRM授權伺服器工作階段。

**授權管理**

每當裝置播放受保護的內容時，執行階段就會取得並快取檢視內容所需的授權。 如果應用程式將內容儲存在本機，且授權允許離線播放，則使用者無需網路連線即可檢視應用程式中的內容。 使用 `DRMManager`，您可以預先快取授權。 應用程式不需要取得檢視內容所需的授權。 例如，您的應用程式可以下載媒體檔案，然後在使用者仍然線上上時取得授權。

若要預先載入授權，請使用 `DRMContentData` 物件。 此 `DRMContentData` 物件包含Primetime DRM許可證伺服器的URL，可提供許可證並描述是否需要使用者驗證。 有了這些資訊，您可以呼叫 `DRMManager` `loadVoucher()` 取得和快取授權的方法。 如需預先載入授權的工作流程，請參閱以下章節： *預先載入離線播放的授權*.

**工作階段管理**

您也可以使用 `DRMManager` 驗證使用者對Primetime DRM授權伺服器的身份並管理持續工作階段。 呼叫 `DRMManager` `authenticate()` 與Primetime DRM授權伺服器建立工作階段的方法。 成功完成驗證時， `DRMManager` 傳送 `DRMAuthenticationCompleteEvent` 物件。 此物件包含工作階段權杖。 您可以儲存此Token以建立未來的工作階段，讓使用者不必提供其帳戶認證。 將權杖傳遞至 `setAuthenticationToken()` 建立新的已驗證工作階段的方法。 （產生權杖的伺服器的設定會決定權杖到期日和其他屬性）。

## 處理DRMStatus事件 {#handling-drmstatus-events}

此 `DRMManager` 傳送 `DRMStatusEvent` 呼叫後的物件 `loadVoucher()` 方法成功完成。 如果取得授權，則事件物件的detail屬性的值如下： `DRM.voucherObtained`，而voucher屬性包含 `DRMVoucher` 物件。 如果未取得授權，則detail屬性仍有值： `DRM.voucherObtained`；不過，憑單屬性為null。 例如，如果您使用 `LoadVoucherSetting` 之 `localOnly` 而且沒有本機快取的授權。 如果 `loadVoucher()` 呼叫未成功完成，可能是因為驗證或通訊錯誤，然後 `DRMManager` 傳送 `DRMErrorEvent` 或 `DRMAuthenticationErrorEvent` 物件。

## 處理DRMAuthenticationComplete事件{#handling-drmauthenticationcomplete-events}

此 `DRMManager` 傳送 `DRMAuthenticationCompleteEvent` 物件（當透過呼叫成功驗證使用者時） `authenticate()` 方法。 此 `DRMAuthenticationCompleteEvent` 物件包含可重複使用的權杖，可用於跨應用程式工作階段儲存使用者驗證。 將此權杖傳遞至 `DRMManager` `setAuthenticationToken()` 重新建立工作階段的方法。 (權杖建立者會設定權杖屬性，例如到期。 Adobe未提供用於檢查Token屬性的API。)

## 處理DRMAuthenticationError事件{#handling-drmauthenticationerror-events}

此 `DRMManager` 傳送 `DRMAuthenticationErrorEvent` 當無法透過對的呼叫成功驗證使用者時的物件 `authenticate()` 或 `setAuthenticationToken()` 方法。
