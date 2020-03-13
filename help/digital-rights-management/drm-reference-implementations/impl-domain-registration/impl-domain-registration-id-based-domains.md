---
description: 'null'
seo-description: 'null'
seo-title: 基於身份的域註冊邏輯
title: 基於身份的域註冊邏輯
uuid: bc13f7c2-9a20-4f80-b96f-05f7a0fcc343
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 基於身份的域註冊邏輯{#identity-based-domain-registration-logic}

## 域註冊邏輯 {#section_149C247458954877AF158B4A09A8526B}

參考實作對基於身份的域註冊應用以下邏輯：

1. 確定要分配給指定用戶的域名。

   網域名稱( `namequalifier:username`)從驗證Token中擷取。 如果Token不可用，則會擲回錯誤。
1. 在表格中查找域 `DomainServerInfo` 名。

   如果未找到任何條目，請插入條目。 預設值為：

   * `authentication required`
   * `max domain membership=5`
   .

1. 要驗證設備是否已向域註冊：

   1. 查看表 `domainname` 格中 `UserDomainMembership` 的：

      1. 對於所找到的每個機器ID，請比較該ID與請求中的機器ID。
      1. 如果這是新機器，請將條目添加到表 `UserDomainMembership` 中。
      1. 在表中搜索匹配 `UserDomainRefCount` 記錄。
      1. 如果此電腦GUID不存在條目，請添加記錄。
   1. 如果是新裝置，且已 `Max Membership` 到達值，則傳回錯誤。


1. 在表中查找此域的所有域 `DomainKeys` 鍵：

   1. 如果 `DomainServerInfo` 指出需要轉換密鑰，請生成新密鑰對，
   1. 將對保存在表 `DomainKeys` 中，其密鑰版本高於現有最高密鑰的一個。
   1. 在中重 `Key Rollover Required` 設標幟 `DomainServerInfo`。

   1. 對於每個域密鑰，生成域憑據。

## 域取消註冊邏輯 {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

參考實施對基於身份的域取消註冊應用以下邏輯：

1. 確定要分配給此用戶的域名。

   域名是從 `namequalifier:username`驗證令牌中提取的。 如果沒有可用的Token，則會發生傳回 `DOM_AUTHENTICATION_REQUIRED (503)` 錯誤。
1. 在表格中查找請求的域 `DomainServerInfo` 名。
1. 在表格中查找域 `UserDomainMembership` 名。
1. 比較您找到的每個電腦ID與請求中的電腦ID。
1. 在表中找到相應的 `UserDomainRefCount` 條目。

   如果找不到相符的項目，則返回錯誤。

1. 如果這不是預覽請求，請從表格中刪除該 `UserDomainRefCount` 條目。
1. 如果該表中沒有該電腦的其他條目，請從中刪除該條目 `UserDomainMembership` 並在屬 [!DNL Key Rollover Required] 性中設定標 `DomainServerInfo` 志。

每位使用者都可註冊少量的電腦，因此您可以使用完整的電腦ID和方 `matches()` 法來計算電腦。 由於使用者可多次註冊，因此伺服器需要透過不同瀏覽器中的多個AIR應用程式或播放器，以維持參考計數，以便也可計算取消註冊。

>[!NOTE]
>
>在放棄機器上的所有網域Token之前，取消註冊尚未完成。

