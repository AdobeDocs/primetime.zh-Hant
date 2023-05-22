---
title: 匿名域邏輯
description: 匿名域邏輯
copied-description: true
exl-id: 4a6c3485-cde7-403f-89d8-f6420df3539a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 匿名域邏輯{#anonymous-domain-logic}

## 域註冊邏輯 {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

該引用實現對匿名域註冊應用以下邏輯：

1. 從請求URL分析域名。
1. 在 `DomainServerInfo` 的子菜單。
1. 如果找不到條目，請在表中插入條目。

   預設值為：

   * `authentication is not required`
   * `no membership maximum`

   如果請求的域需要驗證，請確保請求中包含有效的驗證令牌。 如果在資料庫中指定了身份驗證命名空間，則令牌必須與指定的身份驗證命名空間匹配。
1. 如果需要身份驗證，但無效的身份驗證令牌可用，則返回錯誤 `DOM_AUTHENTICATION_REQUIRED (503)`。
1. 檢查設備是否已向域註冊：

   1. 在 `DomainMembership` 的子菜單。
   1. 將您找到的電腦GUID與請求中的電腦GUID進行比較。
   1. 如果這是新電腦，請在 `DomainMembership` 的子菜單。
   1. 如果是新設備， `Max Membership` 已達到值，返回錯誤 `DOM_LIMIT_REACHED (502)`。

1. 查找此域的所有域密鑰 `DomainKeys` 表：

   1. 如果 `DomainServerInfo` 指示需要滾動密鑰，生成新密鑰對。
   1. 將鍵對保存到 `DomainKeys` 表，其鍵版本比現有的最高鍵高一個數。
   1. 重置 `Key Rollover Required` 標誌 `DomainServerInfo`。

   1. 對於每個域密鑰，生成域憑據。

## 域註銷邏輯 {#section_C968BBFCBFAB4510A903D169F38C9FCE}

引用實現對匿名域取消註冊應用以下邏輯：

1. 從請求URL分析域名。
1. 在 `DomainServerInfo` 的子菜單。
1. 如果請求的域需要身份驗證，請確保請求中包含有效的身份驗證令牌。

   令牌還必須與在資料庫中指定的身份驗證命名空間匹配。
1. 在中查找域名和電腦GUID `DomainMembership` 的子菜單。

   如果找不到匹配項，則返回錯誤 `DEREG_DENIED (401)`。

1. 如果這不是預覽請求，請從 `DomainMembership`中 `DomainServerInfo`的子菜單。 `Key Rollover Required` 。

由於許多電腦可能加入域，因此不能簡單地與電腦ID匹配。 而是應用在個性化過程中分配給電腦的隨機電腦GUID。
