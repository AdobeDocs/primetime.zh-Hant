---
title: 使用DRMManager類概述
description: 使用DRMManager類概述
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# 使用DRMManager類 {#using-the-drmmanager-class}

使用 `DRMManager` 類，用於管理應用程式中的許可證和Mighine DRM許可證伺服器會話。

**許可證管理**

每當設備播放受保護的內容時，運行時就獲取並快取查看內容所需的許可證。 如果應用程式將內容本地保存，並且許可證允許離線回放，則用戶可以在沒有網路連接的情況下查看應用程式中的內容。 使用 `DRMManager`，您可以預快取許可證。 應用程式不必獲得查看內容所需的許可證。 例如，您的應用程式可以下載媒體檔案，然後在用戶仍線上時獲取許可證。

要預載入許可證，請使用 `DRMContentData` 的雙曲餘切值。 的 `DRMContentData` 對象包含Mogfire DRM許可證伺服器的URL，該伺服器可提供許可證並描述是否需要用戶驗證。 通過這些資訊，您可以 `DRMManager` `loadVoucher()` 獲取和快取許可證的方法。 對預載入許可證的工作流進行了更詳細的描述，如 *預載入用於離線播放的許可證*。

**會話管理**

您還可以使用 `DRMManager` 將用戶驗證到Mogfire DRM許可證伺服器並管理持久會話。 呼叫 `DRMManager` `authenticate()` 一種與黃金時段DRM許可伺服器建立會話的方法。 成功完成身份驗證後， `DRMManager` 派單 `DRMAuthenticationCompleteEvent` 的雙曲餘切值。 此對象包含會話令牌。 您可以保存此令牌以建立將來的會話，這樣用戶就不必提供其帳戶憑據。 將令牌傳遞給 `setAuthenticationToken()` 建立新的已驗證會話的方法。 （生成令牌的伺服器的設定決定了令牌過期和其他屬性）。

## 處理DRMStatus事件 {#handling-drmstatus-events}

的 `DRMManager` 派單 `DRMStatusEvent` 調用後的對象 `loadVoucher()` 方法成功完成。 如果獲取了許可證，則事件對象的detail屬性的值為： `DRM.voucherObtained`，並且憑證屬性包含 `DRMVoucher` 的雙曲餘切值。 如果未獲取許可證，則detail屬性仍具有以下值： `DRM.voucherObtained`;但是，憑證屬性為null。 例如，如果使用 `LoadVoucherSetting` 共 `localOnly` 並且沒有本地快取的許可證。 如果 `loadVoucher()` 呼叫未成功完成，可能是由於身份驗證或通信錯誤，然後 `DRMManager` 派單 `DRMErrorEvent` 或 `DRMAuthenticationErrorEvent` 的雙曲餘切值。

## 處理DRMAuthenticationComplete事件{#handling-drmauthenticationcomplete-events}

的 `DRMManager` 派單 `DRMAuthenticationCompleteEvent` 當用戶通過調用成功驗證對象時 `authenticate()` 的雙曲餘切值。 的 `DRMAuthenticationCompleteEvent` 對象包含可重用的令牌，可用於跨應用程式會話持續用戶身份驗證。 將此令牌傳遞給 `DRMManager` `setAuthenticationToken()` 重新建立會話的方法。 (令牌建立者設定令牌屬性，如過期。 Adobe不提供用於檢查令牌屬性的API。)

## 處理DRMAuthenticationError事件{#handling-drmauthenticationerror-events}

的 `DRMManager` 派單 `DRMAuthenticationErrorEvent` 用戶無法通過調用成功驗證對象時 `authenticate()` 或 `setAuthenticationToken()` 的雙曲餘切值。