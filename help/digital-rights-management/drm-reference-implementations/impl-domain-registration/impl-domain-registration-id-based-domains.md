---
title: 以身分為基礎的網域註冊邏輯
description: 以身分為基礎的網域註冊邏輯
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 以身分為基礎的網域註冊邏輯{#identity-based-domain-registration-logic}

## 網域註冊邏輯 {#section_149C247458954877AF158B4A09A8526B}

此參考實作會套用下列邏輯進行以身分為基礎的網域註冊：

1. 決定要指派給指定使用者的網域名稱。

   網域名稱( `namequalifier:username`)擷取自驗證Token。 如果權杖無法使用，則會擲回錯誤。
1. 在中查詢網域名稱 `DomainServerInfo` 表格。

   如果找不到專案，請插入專案。 預設值為：

   * `authentication required`
   * `max domain membership=5`

   .

1. 若要確認裝置已在網域註冊：

   1. 查詢 `domainname` 在 `UserDomainMembership` 表格：

      1. 針對找到的每個機器ID，將ID與請求中的機器ID進行比較。
      1. 如果這是新電腦，請將專案新增至 `UserDomainMembership` 表格。
      1. 搜尋中的相符記錄 `UserDomainRefCount` 表格。
      1. 如果此電腦GUID沒有專案，請新增記錄。

   1. 如果是新裝置，而且 `Max Membership` 已達到值，傳回錯誤。

1. 在「 」中查詢此網域的所有網域金鑰 `DomainKeys` 表格：

   1. 如果 `DomainServerInfo` 表示金鑰必須翻轉，產生新的金鑰組，
   1. 將配對儲存在 `DomainKeys` 資料表，其索引鍵版本比最高的現有索引鍵高1。
   1. 重設 `Key Rollover Required` 標幟於 `DomainServerInfo`.

   1. 對於每個網域金鑰，產生網域認證。

## 網域取消註冊邏輯 {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

此參考實作會套用下列邏輯進行以身分為基礎的網域取消註冊：

1. 決定要指派給此使用者的網域名稱。

   網域名稱是 `namequalifier:username`，這會從驗證Token擷取。 如果沒有Token可用，則傳回錯誤 `DOM_AUTHENTICATION_REQUIRED (503)` 發生。
1. 在中查詢請求的網域名稱 `DomainServerInfo` 表格。
1. 在中查詢網域名稱 `UserDomainMembership` 表格。
1. 將您找到的每個電腦ID與請求中的電腦ID進行比較。
1. 在「 」中找到對應的專案 `UserDomainRefCount` 表格。

   如果找不到相符的專案，則會傳回錯誤。

1. 如果這不是預覽請求，請從刪除專案 `UserDomainRefCount` 表格。
1. 如果該電腦的表格中沒有其他專案，請從中刪除該專案 `UserDomainMembership` 並設定 [!DNL Key Rollover Required] 中的標幟 `DomainServerInfo` 屬性。

每位使用者可註冊少量電腦，因此您可以使用完整的電腦ID和 `matches()` 計數電腦的方法。 由於使用者可以多次註冊，透過多個AIR應用程式或不同瀏覽器中的播放器，伺服器需要維持參考計數，以便也可以計算取消註冊的數量。

>[!NOTE]
>
>除非交出電腦上的所有網域權杖，否則取消註冊不會完成。
