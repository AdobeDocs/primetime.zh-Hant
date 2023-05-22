---
title: 基於身份的域
description: 基於身份的域
copied-description: true
exl-id: de7b6c8a-5227-4679-933a-3278921903d7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# 基於身份的域 {#identity-based-domains}

在這種使用情況下，每個經過身份驗證的用戶都有自己的域，並且允許一定數量的設備加入域。 要將此類型的域與引用實現一起使用，需要建立指定域註冊的策略。 指定域伺服器URL的伺服器主機和埠，並指定需要用戶名/密碼驗證。

該引用實現實現以下域註冊邏輯：

1. 確定要分配給此用戶的域名。 域名將為* `namequalifier:username`*從驗證令牌中提取。 如果沒有驗證令牌，則返回錯誤DOM_AUTHENTICATION_REQUIRED(503)。
1. 查找中的域名 `DomainServerInfo` 的子菜單。 如果找不到條目，請將條目插入表（預設值為需要驗證，最大域成員資格=5）。
1. 檢查設備是否已向域註冊：

   1. 查找中的域名 `UserDomainMembership` 的子菜單。 對於找到的每個電腦ID，請與請求中的電腦ID進行比較。 如果這是新電腦，請向 `UserDomainMembership` 的子菜單。 接下來，在 `UserDomainRefCount` 的子菜單。 如果此電腦GUID不存在條目，請添加記錄。

   1. 如果是新設備，並且已達到最大成員資格，則返回錯誤DOM_LIMIT_MACHEENT(502)。

1. 在DomainKeys表中查找此域的所有域密鑰。

   1. 如果 `DomainServerInfo` 指示需要滾動鍵、生成新鍵對，並將其保存到 `DomainKeys` 表（密鑰版本1高於現有最高密鑰），並在中重置「需要密鑰滾動更新」標誌 `DomainServerInfo`。

   1. 對於每個域密鑰，生成域憑據。

引用實現，實現了以下域註銷邏輯：

1. 確定要分配給此用戶的域名。 域名將是 *名稱限定符：用戶名* 從驗證令牌中提取。 如果沒有驗證令牌，則返回錯誤DOM_AUTHENTICATION_REQUIRED(503)。
1. 在中查找請求的域名 `DomainServerInfo` 的子菜單。
1. 查找中的域名 `UserDomainMembership` 的子菜單。 對於找到的每個電腦ID，請與請求中的電腦ID進行比較。 在 `UserDomainRefCount` 的子菜單。 如果找不到匹配項，則返回錯誤DEREG_DENIED(401)。

1. 如果這不是預覽請求，請從 `UserDomainRefCount` 的子菜單。 如果該表中沒有該電腦的其他條目，請從中刪除 `UserDomainMembership` 並在中設定「Key Rovel Required（需要密鑰滾動更新）」標誌 `DomainServerInfo`。

在此使用情形中，允許每個用戶註冊少量電腦，因此我們可以使用完整的電腦ID和 `matches()` 精確電腦數的方法。 但是，由於用戶可以在這台機器上註冊多次(通過多個AIR應用程式或不同瀏覽器中的玩家)，因此伺服器還需要維護一個參考計數，以便能夠準確地計算註銷。 取消註冊不能被視為完成，直到電腦上的所有域令牌都被放棄。
