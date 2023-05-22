---
title: 基於身份的域註冊邏輯
description: 基於身份的域註冊邏輯
copied-description: true
exl-id: 6e391fce-00b4-45cf-b785-3b0ec734a11e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 基於身份的域註冊邏輯{#identity-based-domain-registration-logic}

## 域註冊邏輯 {#section_149C247458954877AF158B4A09A8526B}

該參考實現將以下邏輯應用於基於身份的域註冊：

1. 確定要分配給指定用戶的域名。

   域名( `namequalifier:username`)。 如果令牌不可用，則拋出錯誤。
1. 在 `DomainServerInfo` 的子菜單。

   如果找不到條目，請插入條目。 預設值為：

   * `authentication required`
   * `max domain membership=5`

   .

1. 要驗證設備是否已註冊到域：

   1. 查找 `domainname` 的 `UserDomainMembership` 表：

      1. 對於所定位的每個電腦ID，將該ID與請求中的電腦ID進行比較。
      1. 如果這是新電腦，請向 `UserDomainMembership` 的子菜單。
      1. 搜索中的匹配記錄 `UserDomainRefCount` 的子菜單。
      1. 如果此電腦GUID不存在條目，請添加記錄。
   1. 如果是新設備， `Max Membership` 已達到值，返回錯誤。


1. 查找此域的所有域密鑰 `DomainKeys` 表：

   1. 如果 `DomainServerInfo` 指示需要滾動密鑰，生成新密鑰對，
   1. 將對保存到 `DomainKeys` 表，其鍵版本高於現有最高鍵的一個。
   1. 重置 `Key Rollover Required` 標誌 `DomainServerInfo`。

   1. 對於每個域密鑰，生成域憑據。

## 域註銷邏輯 {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

該參考實現為基於身份的域註銷應用以下邏輯：

1. 確定要分配給此用戶的域名。

   域名為 `namequalifier:username`，從驗證令牌中提取。 如果沒有可用的標籤，則返回錯誤 `DOM_AUTHENTICATION_REQUIRED (503)` 。
1. 在 `DomainServerInfo` 的子菜單。
1. 在 `UserDomainMembership` 的子菜單。
1. 將您找到的每個電腦ID與請求中的電腦ID進行比較。
1. 在 `UserDomainRefCount` 的子菜單。

   如果找不到匹配項，則返回錯誤。

1. 如果這不是預覽請求，請從 `UserDomainRefCount` 的子菜單。
1. 如果該表中沒有該電腦的其他條目，請從 `UserDomainMembership` 並設定 [!DNL Key Rollover Required] 標誌 `DomainServerInfo` 屬性。

每個用戶都可以註冊少量電腦，因此您可以使用完整的電腦ID和 `matches()` 電腦計數的方法。 由於用戶可以多次註冊，通過多個AIR應用程式或不同瀏覽器中的玩家，伺服器需要維護一個引用計數，以便還可以計算註銷。

>[!NOTE]
>
>取消註冊在電腦上的所有域令牌都放棄之前不會完成。
