---
title: 匿名網域
description: 匿名網域
copied-description: true
exl-id: a9358582-ad25-4016-94d2-cd82b4c00573
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 匿名網域 {#anonymous-domains}

在此使用案例中，大量裝置屬於單一網域，且可能不需要驗證。 若要將此型別的網域用於參考實作，請建立指定需要網域註冊的原則。 將網域伺服器URL指定為 `https:// host:port/flashaccess/domainserver/domainname/` 和指定匿名驗證。

參考實作會實作下列網域註冊的邏輯：

1. 從請求URL剖析網域名稱。
1. 在中查詢網域名稱 `DomainServerInfo` 表格。 如果找不到專案，請在表格中插入專案（預設值：不需要驗證，也沒有成員資格上限）。
1. 如果要求的網域需要驗證，請確定請求中包含有效的驗證權杖，並比對驗證名稱空間（如果在資料庫中指定）。

   1. 如果需要驗證，但未提供有效的驗證權杖，則會傳回錯誤 `DOM_AUTHENTICATION_REQUIRED (503)`.

1. 檢查裝置是否已向網域註冊：

   1. 在中查詢網域名稱 `DomainMembership` 表格。 針對找到的每個電腦GUID，請和請求中的電腦GUID進行比較。 如果這是新電腦，請將專案新增至 `DomainMembership` 表格。

   1. 如果是新裝置，且已達到最大成員資格，則會傳回錯誤 `DOM_LIMIT_REACHED (502)`.

1. 在「 」中查詢此網域的所有網域金鑰 `DomainKeys` 表格。

   1. 若 `DomainServerInfo` 表示需要捲動金鑰，產生新的金鑰組，並將其儲存在 `DomainKeys` 表格（金鑰版本比現有最高金鑰版本高一），並重設 `Key Rollover Required` 標幟於 `DomainServerInfo`.

   1. 對於每個網域金鑰，產生網域認證。

參考實作會實作下列網域解除註冊的邏輯：

1. 從請求URL剖析網域名稱。
1. 在中查詢要求的網域名稱 `DomainServerInfo` 表格。
1. 如果要求的網域需要驗證，請確定請求中包含有效的驗證權杖，並比對驗證名稱空間（如果在資料庫中指定）。
1. 在中查詢網域名稱和電腦GUID `DomainMembership` 表格。 如果找不到相符的專案，則傳回錯誤 `DEREG_DENIED (401)`.

1. 如果這不是預覽請求，請從刪除專案 `DomainMembership` 並設定 `Key Rollover Required` 標幟於 `DomainServerInfo`.

在此使用案例中，由於大量電腦可以加入網域，因此不可能完全符合電腦ID。 而是使用在個人化期間指派給機器的隨機機器GUID。
