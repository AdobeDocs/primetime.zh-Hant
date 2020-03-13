---
description: 「權益管理員」是支援Primetime驗證實作的功能管理員。
seo-description: 「權益管理員」是支援Primetime驗證實作的功能管理員。
seo-title: 權益管理員概述
title: 權益管理員概述
uuid: b33dfae3-a132-4215-9992-80cbf4c87a61
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 權益管理員概述 {#entitlement-manager-overview}

「權益管理員」是支援Primetime驗證實作的功能管理員。

## 功能概觀

與Android Primetime SDK參考實作整合的Primetime驗證為應用程式新增了功能管理員。 不過，與許多其他功能管理員不同， *EntitlementManager會在應用程式的數個位置使用*。 以下概述對「參考實作」所做的變更和新增，以支援Primetime驗證：

### EntitlementManager類別

此類 `EntitlementManager` 別可處理與Primetime驗證SDK的所有通訊，並封裝權益工作流程所需的應用程式邏輯。 應 `EntitlementManager`用程式會使用公用API來啟動權益工作流程，而介面會為應用程式提供回呼機制，以處理 `EntitlementMangerListener``EntitlementManger` 事件。

### EntitlementManager回呼

「參考實作」的主要活動( `CatalogActivity`)會建立例項，並 `EntitlementManagerListener` 將其註冊到 `EntitlementManager`。 如此，該應用程 `EntitlementManager` 式可能會傳達其他應用程式所需的UI更新。 回呼包括顯示／隱藏載入對話框、顯示狀態對話框、更新授權和驗證圖示，以及在成功授權時啟動視訊播放。

### 權益對話框

類別 `EntitlementDialogFragment` 會根據傳遞至類別建構函式的權益狀態產生對話訊息。 此類用於驗證成功消息和所有錯誤消息。 當權 `CatalogActivity` 益對話方塊收到來自的特定事件時，就會顯示 `EntitlementManager`。 此外，該介 `CatalogActivity` 面包括回 `EntitlementDialogListener` 呼方法，以在對話方塊關閉或使用者從Primetime驗證服務登出時發出訊號。

### 內容提供者選擇與登入

在使用Primetime驗證進行驗證期間，有兩 `MvpdPickerActivity` 個新活 `MvpdLoginActivity`動可讓使用者選擇其內容提供者並登入。 這兩個活動都從通過 `CatalogActivity` 開始 `EntitlementManager`。 此外，將結 `MvpdPickerActivity` 果和 `MvpdLoginActivity` 返回結果都返回 `CatalogActivity` ，因此 `CatalogActivity` 必須覆蓋方 `Activity.onActivityResult` 法。

### 登入按鈕

「參考實作」的主要活動( `CatalogActivity`)在其動作列中包含新的「登入」按鈕。 「登入」按鈕可讓使用者使用Primetime驗證來啟動驗證。 此外，用戶可以通過選擇受保護的視頻來發起驗證。 「登入」按鈕的圖示和文字會隨使用者的驗證狀態而變更，而且包含的程式碼會在頁面重新整理時更新按鈕的圖示和文字。 `CatalogActivity` 若要這麼做，啟動時 `CatalogActivity` 會呼叫以 `EntitlementManager.checkAuthentication()` 更新使用者的驗證狀態。

### 內容權益

在中， `CatalogView`新圖示會顯示在內容圖示的上方，以指示使用者對該內容的授權狀態。 例如，如果使用者已預先取得檢視視訊的授權，則內容上會顯示綠色圓圈圖示。 不過，如果使用者未預先取得檢視視訊的授權，則會顯示按鍵圖示。 這些圖示的顯示會在中 `ContentTileAdapter`處理，但是，其狀態的更新會從呼叫中 `CatalogActivity` 的回呼開始 `EntitlementManagerListener` 進行。

### 內容播放

現在，視訊播放需要由進行授權檢查 `EntitlementManager`。 在中發 `EntitlementManager.getAuthorization()` 生呼叫 `CatalogView`。 如果視訊需要授權且使用者已授權， `PlayerActivity` 則從啟動 `CatalogActivity`。

