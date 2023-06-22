---
description: 權利管理員是功能管理員，可支援Primetime驗證實作。
title: 軟體權利檔案管理員概述
exl-id: a66e131e-283f-4378-b834-7cfa887b3ec9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# 軟體權利檔案管理員概述 {#entitlement-manager-overview}

權利管理員是功能管理員，可支援Primetime驗證實作。

## 功能概述

Primetime驗證與Android Primetime SDK Reference實作整合，為應用程式新增了功能管理員。 不過，與其他許多功能管理員不同， *EntitlementManager會在整個應用程式的多個位置使用*. 以下提供支援Primetime驗證的「參考實作」變更和新增內容的概觀：

### EntitlementManager類別

此 `EntitlementManager` 類別會處理與Primetime驗證SDK的所有通訊，而且會封裝權利工作流程所需的應用程式邏輯。 此 `EntitlementManager`應用程式會使用公開API來起始權益工作流程，而 `EntitlementMangerListener` 介面為應用程式處理提供回呼機制 `EntitlementManger` 事件。

### EntitlementManger回呼

參考實作的主要活動 `CatalogActivity`，建立例項 `EntitlementManagerListener` 並註冊給 `EntitlementManager`. 如此一來， `EntitlementManager` 可能表示應用程式的其餘部分需要進行UI更新。 回撥包括顯示/隱藏載入對話方塊、顯示狀態對話方塊、更新授權和驗證圖示，以及在成功授權後開始播放視訊。

### 權益對話方塊

此 `EntitlementDialogFragment` 類別會根據傳遞至類別建構函式的權利狀態產生對話方塊訊息。 此類別用於驗證成功訊息以及所有錯誤訊息。 此 `CatalogActivity` 當從以下位置收到特定事件時顯示軟體權利檔案對話方塊： `EntitlementManager`. 此外， `CatalogActivity` 實作 `EntitlementDialogListener` 介面，包括回呼方法，以在對話方塊關閉或使用者從Primetime驗證服務登出時傳送訊號。

### 內容提供者選擇與登入

在使用Primetime驗證期間，有兩個新活動， `MvpdPickerActivity` 和 `MvpdLoginActivity`，可讓使用者選取其內容提供者並登入。 這兩個活動都是從 `CatalogActivity` 透過 `EntitlementManager`. 此外， `MvpdPickerActivity` 和 `MvpdLoginActivity` 將結果傳回 `CatalogActivity` 及因此而 `CatalogActivity` 必須覆寫 `Activity.onActivityResult` 方法。

### 登入按鈕

參考實作的主要活動 `CatalogActivity`，在動作列中放入新的「登入」按鈕。 「登入」按鈕可讓使用者啟動具有Primetime驗證的驗證。 此外，使用者可以選取要播放的受保護視訊來起始驗證。 登入按鈕的圖示和文字會隨著使用者的驗證狀態和 `CatalogActivity` 包含頁面重新整理時更新按鈕圖示和文字的程式碼。 若要這麼做，當 `CatalogActivity` 開始，它會呼叫 `EntitlementManager.checkAuthentication()` 更新使用者的驗證狀態。

### 內容權利

在內 `CatalogView`，內容圖示上方會顯示新圖示，以表示該內容的使用者授權狀態。 例如，如果使用者預先獲得觀看視訊的授權，則內容上方會顯示綠色圓圈圖示。 但是，如果使用者未獲得檢視視訊的預授權，則會顯示一個鍵圖示。 這些圖示的顯示方式處理於 `ContentTileAdapter`但是，其狀態的更新是從以下專案啟動： `CatalogActivity` 當回呼位於 `EntitlementManagerListener` 稱為。

### 內容播放

視訊播放現在需要由進行授權檢查 `EntitlementManager`. 對的呼叫 `EntitlementManager.getAuthorization()` 發生於 `CatalogView`. 如果影片需要授權且使用者已獲得授權， `PlayerActivity` 開始於 `CatalogActivity`.
