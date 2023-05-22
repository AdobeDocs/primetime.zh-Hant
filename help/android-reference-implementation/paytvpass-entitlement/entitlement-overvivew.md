---
description: 權利管理器是支援黃金時段身份驗證實現的功能管理器。
title: 權利檔案管理器概述
exl-id: a66e131e-283f-4378-b834-7cfa887b3ec9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# 權利檔案管理器概述 {#entitlement-manager-overview}

權利管理器是支援黃金時段身份驗證實現的功能管理器。

## 功能概述

黃金時段認證與Android Mighine SDK參考實現的整合為應用程式添加了一個新的功能管理器。 但是，與許多其他功能管理器不同， *在應用程式的多個位置使用EntilementManager*。 下面概述了為支援黃金時段身份驗證而對參考實施所做的更改和補充：

### EntitlementManager類

的 `EntitlementManager` 類處理與Gimfire身份驗證SDK的所有通信，並封裝權利工作流所需的應用程式邏輯。 的 `EntitlementManager`應用程式使用的公共API來啟動權利工作流，而 `EntitlementMangerListener` 介面為應用程式提供回調機制以處理 `EntitlementManger` 事件。

### EntitlementManger回調

參考實施的主要活動， `CatalogActivity`，建立的實例 `EntitlementManagerListener` 並註冊到 `EntitlementManager`。 這樣， `EntitlementManager` 可能會向應用程式的其餘部分發出所需的UI更新信號。 回叫包括顯示/隱藏載入對話框、顯示狀態對話框、更新授權和驗證表徵圖，以及在成功授權時啟動視頻回放。

### 權利對話框

的 `EntitlementDialogFragment` 類根據傳遞給類建構子的權利狀態生成對話框消息。 此類用於驗證成功消息和所有錯誤消息。 的 `CatalogActivity` 在收到來自 `EntitlementManager`。 另外， `CatalogActivity` 實現 `EntitlementDialogListener` 介面，包括當對話框關閉或用戶從Gimfire認證服務註銷時發出信號的回調方法。

### 內容提供方選擇和登錄

在使用Mighine驗證進行驗證期間，有兩個新活動， `MvpdPickerActivity` 和 `MvpdLoginActivity`，允許用戶選擇其內容提供商和登錄。 這兩個活動都從 `CatalogActivity` 通過 `EntitlementManager`。 此外， `MvpdPickerActivity` 和 `MvpdLoginActivity` 將結果返回到 `CatalogActivity` 因此 `CatalogActivity` 必須覆蓋 `Activity.onActivityResult` 的雙曲餘切值。

### 登錄按鈕

參考實施的主要活動， `CatalogActivity`，在其操作欄中包含新的「登錄」按鈕。 「登錄」按鈕允許用戶使用黃金時段驗證啟動驗證。 另外，用戶可以通過選擇用於回放的受保護視頻來啟動驗證。 「登錄」按鈕的表徵圖和文本會根據用戶的身份驗證狀態和 `CatalogActivity` 包含代碼，以在頁面刷新時更新按鈕的表徵圖和文本。 當 `CatalogActivity` 開始，它調用 `EntitlementManager.checkAuthentication()` 更新用戶的身份驗證狀態。

### 內容權利

在 `CatalogView`，新表徵圖顯示在內容表徵圖的頂部，以指示用戶對該內容的授權狀態。 例如，如果用戶已經預先授權查看視頻，則在內容上顯示綠色圓表徵圖。 但是，如果用戶未獲得觀看視頻的預授權，則顯示一個鍵表徵圖。 這些表徵圖的顯示在 `ContentTileAdapter`但是，其狀態的更新是從 `CatalogActivity` 當回電時 `EntitlementManagerListener` 。

### 內容播放

現在，視頻播放需要通過 `EntitlementManager`。 呼叫 `EntitlementManager.getAuthorization()` 發生 `CatalogView`。 如果視頻需要授權且用戶已授權， `PlayerActivity` 從 `CatalogActivity`。
