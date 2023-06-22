---
title: 匿名網域邏輯
description: 匿名網域邏輯
copied-description: true
exl-id: 4a6c3485-cde7-403f-89d8-f6420df3539a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 匿名網域邏輯{#anonymous-domain-logic}

## 網域註冊邏輯 {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

參考實作會將下列邏輯套用到匿名網域註冊：

1. 從請求URL剖析網域名稱。
1. 在中查詢網域名稱 `DomainServerInfo` 表格。
1. 如果找不到專案，請在表格中插入專案。

   預設值為：

   * `authentication is not required`
   * `no membership maximum`

   如果請求的網域需要驗證，請確保請求中包含有效的驗證Token。 如果在資料庫中指定了驗證名稱空間，代號必須符合指定的驗證名稱空間。
1. 如果需要驗證，但沒有有效的驗證權杖可用，則傳回錯誤 `DOM_AUTHENTICATION_REQUIRED (503)`.
1. 檢查裝置是否已向網域註冊：

   1. 在中查詢網域名稱 `DomainMembership` 表格。
   1. 將您找到的電腦GUID與請求中的電腦GUID進行比較。
   1. 如果這是新電腦，請在 `DomainMembership` 表格。
   1. 如果是新裝置且 `Max Membership` 已達到值，傳回錯誤 `DOM_LIMIT_REACHED (502)`.

1. 在「 」中查詢此網域的所有網域金鑰 `DomainKeys` 表格：

   1. 若 `DomainServerInfo` 表示需要捲動金鑰，並產生新的金鑰組。
   1. 將金鑰組儲存在 `DomainKeys` 表格，其金鑰版本比現有金鑰的最高版本高一個數字。
   1. 重設 `Key Rollover Required` 標幟於 `DomainServerInfo`.

   1. 對於每個網域金鑰，產生網域認證。

## 網域取消註冊邏輯 {#section_C968BBFCBFAB4510A903D169F38C9FCE}

參考實作會套用下列邏輯來取消註冊匿名網域：

1. 從請求URL剖析網域名稱。
1. 在中查詢要求的網域名稱 `DomainServerInfo` 表格。
1. 如果請求的網域需要驗證，請確保請求中包含有效的驗證Token。

   代號也必須符合資料庫中指定的驗證名稱空間。
1. 在中查詢網域名稱和電腦GUID `DomainMembership` 表格。

   如果找不到相符的專案，則會傳回錯誤 `DEREG_DENIED (401)`.

1. 如果這不是預覽請求，請從刪除專案 `DomainMembership`、和 `DomainServerInfo`，設定 `Key Rollover Required` 標幟。

由於大量電腦可能會加入網域，因此您無法僅比對電腦ID。 而是套用個人化期間指派給機器的隨機機器GUID。
