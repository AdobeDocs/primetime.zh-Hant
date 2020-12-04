---
description: 'null'
seo-description: 'null'
seo-title: 基於身份的域註冊邏輯
title: 基於身份的域註冊邏輯
uuid: bc13f7c2-9a20-4f80-b96f-05f7a0fcc343
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---


# 基於身份的域註冊邏輯{#identity-based-domain-registration-logic}

## 域註冊邏輯{#section_149C247458954877AF158B4A09A8526B}

參考實作對基於身份的域註冊應用以下邏輯：

1. 確定要分配給指定用戶的域名。

   網域名稱(`namequalifier:username`)會從驗證Token中擷取。 如果Token不可用，則會擲回錯誤。
1. 在`DomainServerInfo`表中查找域名。

   如果未找到任何條目，請插入條目。 預設值為：

   * `authentication required`
   * `max domain membership=5`

   .

1. 要驗證設備是否已向域註冊：

   1. 查看`UserDomainMembership`表中的`domainname` :

      1. 對於所找到的每個機器ID，請比較該ID與請求中的機器ID。
      1. 如果這是新機器，請將條目添加到`UserDomainMembership`表中。
      1. 在`UserDomainRefCount`表中搜索匹配記錄。
      1. 如果此電腦GUID不存在條目，請添加記錄。
   1. 如果是新設備，且已到達`Max Membership`值，則返回錯誤。


1. 在`DomainKeys`表中查找此域的所有域鍵：

   1. 如果`DomainServerInfo`指出需要滾動鍵，請生成新鍵對，
   1. 將對保存在`DomainKeys`表中，其密鑰版本比現有的最高密鑰版本高一。
   1. 重設`DomainServerInfo`中的`Key Rollover Required`標幟。

   1. 對於每個域密鑰，生成域憑據。

## 域取消註冊邏輯{#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

參考實施對基於身份的域取消註冊應用以下邏輯：

1. 確定要分配給此用戶的域名。

   網域名稱為`namequalifier:username`，會從驗證Token中擷取。 如果沒有可用的標籤，則會發生傳回錯誤`DOM_AUTHENTICATION_REQUIRED (503)`。
1. 在`DomainServerInfo`表中查找請求的域名。
1. 在`UserDomainMembership`表中查找域名。
1. 比較您找到的每個電腦ID與請求中的電腦ID。
1. 在`UserDomainRefCount`表中找到相應的條目。

   如果找不到相符的項目，則返回錯誤。

1. 如果這不是預覽請求，請從`UserDomainRefCount`表格中刪除該條目。
1. 如果該表中沒有該電腦的其他條目，請從`UserDomainMembership`中刪除該條目，並在`DomainServerInfo`屬性中設定[!DNL Key Rollover Required]標誌。

每個用戶都可以註冊少量的電腦，因此您可以使用完整的電腦ID和`matches()`方法來計算電腦。 由於使用者可多次註冊，因此伺服器需要透過不同瀏覽器中的多個AIR應用程式或播放器，以維持參考計數，以便也可計算取消註冊。

>[!NOTE]
>
>在放棄機器上的所有網域Token之前，取消註冊尚未完成。

