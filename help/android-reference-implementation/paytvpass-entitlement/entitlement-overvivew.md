---
description: 「權益管理員」是支援Primetime驗證實作的功能管理員。
title: 權益管理員概述
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# 權益管理員概觀{#entitlement-manager-overview}

「權益管理員」是支援Primetime驗證實作的功能管理員。

## 功能概觀

與Android Primetime SDK參考實作整合的Primetime驗證為應用程式新增了功能管理員。 不過，與許多其他功能管理員不同，*EntitlementManager會用於應用程式中的數個位置。*&#x200B;以下概述對「參考實作」所做的變更和新增，以支援Primetime驗證：

### EntitlementManager類別

`EntitlementManager`類別可處理與Primetime驗證SDK的所有通訊，並封裝權益工作流程所需的應用程式邏輯。 應用程式會使用`EntitlementManager`的公用API來啟動權益工作流程，而`EntitlementMangerListener`介面則提供回呼機制，讓應用程式處理`EntitlementManger`事件。

### EntitlementManager回呼

參考實作的主要活動`CatalogActivity`會建立`EntitlementManagerListener`的例項，並將它註冊到`EntitlementManager`。 這樣，`EntitlementManager`可能會向應用程式的其餘部分發出所需的UI更新信號。 回呼包括顯示／隱藏載入對話框、顯示狀態對話框、更新授權和驗證圖示，以及在成功授權時啟動視訊播放。

### 權益對話框

`EntitlementDialogFragment`類別會根據傳遞至類別建構函式的權益狀態產生對話訊息。 此類用於驗證成功消息和所有錯誤消息。 當`CatalogActivity`從`EntitlementManager`收到特定事件時，會顯示權益對話方塊。 此外，`CatalogActivity`實作`EntitlementDialogListener`介面，其中包含回呼方法，以在對話方塊關閉或使用者從Primetime驗證服務登出時發出訊號。

### 內容提供者選擇與登入

在使用Primetime驗證進行驗證期間，有兩個新活動`MvpdPickerActivity`和`MvpdLoginActivity`可讓使用者選擇其內容提供者並登入。 這兩個活動都是從`CatalogActivity`經由`EntitlementManager`開始的。 此外，`MvpdPickerActivity`和`MvpdLoginActivity`都會將結果返回至`CatalogActivity`，因此`CatalogActivity`必須覆寫`Activity.onActivityResult`方法。

### 登入按鈕

「參考實作」的主要活動`CatalogActivity`在其動作列中包含新的「登入」按鈕。 「登入」按鈕可讓使用者使用Primetime驗證來啟動驗證。 此外，用戶可以通過選擇受保護的視頻來發起驗證。 「登入」按鈕的圖示和文字會隨使用者的驗證狀態而改變，而`CatalogActivity`包含代碼，可在頁面重新整理時更新按鈕的圖示和文字。 為此，當`CatalogActivity`啟動時，會呼叫`EntitlementManager.checkAuthentication()`以更新使用者的驗證狀態。

### 內容權益

在`CatalogView`中，新圖示會顯示在內容圖示的上方，以顯示該內容的使用者授權狀態。 例如，如果使用者已預先取得檢視視訊的授權，則內容上會顯示綠色圓圈圖示。 不過，如果使用者未預先取得檢視視訊的授權，則會顯示按鍵圖示。 這些圖示的顯示在`ContentTileAdapter`中處理，但是當呼叫`EntitlementManagerListener`中的回呼時，會從`CatalogActivity`開始更新其狀態。

### 內容播放

現在，視訊播放需要`EntitlementManager`的授權檢查。 對`EntitlementManager.getAuthorization()`的調用發生在`CatalogView`內。 如果視訊需要授權且使用者已授權，則`PlayerActivity`會從`CatalogActivity`啟動。

