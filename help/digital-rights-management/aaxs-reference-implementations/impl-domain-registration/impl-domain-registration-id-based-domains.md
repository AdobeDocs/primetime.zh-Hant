---
title: 以身分為基礎的網域
description: 以身分為基礎的網域
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# 以身分為基礎的網域 {#identity-based-domains}

在此使用案例中，每個已驗證的使用者都有自己的網域，並且允許特定數量的裝置加入網域。 若要將此型別的網域用於參考實作，需要建立指定網域註冊的原則。 為網域伺服器URL指定伺服器的主機和連線埠，並指定使用者名稱/密碼驗證為必要項。

參考實作會實作下列網域註冊的邏輯：

1. 決定要指派給此使用者的網域名稱。 網域名稱將會是* `namequalifier:username`*擷取自驗證Token。 如果沒有驗證權杖，傳回錯誤DOM_AUTHENTICATION_REQUIRED (503)。
1. 在中查詢網域名稱 `DomainServerInfo` 表格。 如果找不到專案，請在表格中插入專案（預設值為需要驗證，最大網域成員資格=5）。
1. 檢查裝置是否已向網域註冊：

   1. 在中查詢網域名稱 `UserDomainMembership` 表格。 對於每個找到的電腦ID，請與請求中的電腦ID進行比較。 如果這是新電腦，請將專案新增至 `UserDomainMembership` 表格。 接下來，尋找符合的記錄，位於 `UserDomainRefCount` 表格。 如果此電腦GUID沒有專案，請新增記錄。

   1. 如果是新裝置，而且已達到最大成員資格，則會傳回錯誤DOM_LIMIT_RECEIVED (502)。

1. 在DomainKeys表中查詢此網域的所有網域索引鍵。

   1. 如果 `DomainServerInfo` 表示索引鍵需要捲動，產生新的索引鍵組，並將其儲存在 `DomainKeys` 資料表（金鑰版本比現有金鑰的最高版本高1），並在中重設「需要金鑰變換」標幟 `DomainServerInfo`.

   1. 對於每個網域金鑰，產生網域認證。

在參考實作中，會實作下列網域解除註冊的邏輯：

1. 決定要指派給此使用者的網域名稱。 網域名稱將是 *namequalifier：username* 已從驗證Token擷取。 如果沒有驗證權杖，傳回錯誤DOM_AUTHENTICATION_REQUIRED (503)。
1. 在中查詢要求的網域名稱 `DomainServerInfo` 表格。
1. 在中查詢網域名稱 `UserDomainMembership` 表格。 對於每個找到的電腦ID，請與請求中的電腦ID進行比較。 尋找中的對應專案 `UserDomainRefCount` 表格。 如果找不到相符的專案，則會傳回錯誤DEREG_DENIED (401)。

1. 如果這不是預覽請求，請從刪除專案 `UserDomainRefCount` 表格。 如果該電腦的表格中沒有其他專案，請從中刪除該專案 `UserDomainMembership` 並設定「需要金鑰變換」旗標 `DomainServerInfo`.

在此使用案例中，允許每位使用者註冊少量電腦，以便我們可以使用完整的電腦ID和 `matches()` 精確計算電腦的方法。 不過，由於使用者可以在此電腦上註冊多次(透過多個AIR應用程式或不同瀏覽器中的播放器)，伺服器也需要維持參考計數，以便準確計算取消註冊的數量。 除非交還電腦上的所有網域權杖，否則解除註冊無法被視為完成。
