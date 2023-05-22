---
title: 匿名域
description: 匿名域
copied-description: true
exl-id: a9358582-ad25-4016-94d2-cd82b4c00573
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 匿名域 {#anonymous-domains}

在此使用情況下，大量設備屬於單個域，可能不需要身份驗證。 要將此類型的域與引用實現一起使用，請建立指定需要域註冊的策略。 將域伺服器URL指定為 `https:// host:port/flashaccess/domainserver/domainname/` 並指定匿名驗證。

該引用實現實現以下域註冊邏輯：

1. 從請求URL分析域名。
1. 查找中的域名 `DomainServerInfo` 的子菜單。 如果找不到條目，請將條目插入表(預設值：不需要身份驗證，並且沒有最大成員資格)。
1. 如果請求的域需要身份驗證，請確保請求中包含有效的身份驗證令牌，並與身份驗證命名空間匹配（如果在資料庫中指定）。

   1. 如果需要身份驗證但未提供有效的身份驗證令牌，則返回錯誤 `DOM_AUTHENTICATION_REQUIRED (503)`。

1. 檢查設備是否已向域註冊：

   1. 查找中的域名 `DomainMembership` 的子菜單。 對於找到的每台電腦GUID，請與請求中的電腦GUID進行比較。 如果這是新電腦，請向 `DomainMembership` 的子菜單。

   1. 如果是新設備，並且已達到最大成員資格，則返回錯誤 `DOM_LIMIT_REACHED (502)`。

1. 查找中此域的所有域密鑰 `DomainKeys` 的子菜單。

   1. 如果 `DomainServerInfo` 指示需要滾動的密鑰、生成新的密鑰對、將其保存在 `DomainKeys` 表（密鑰版本1高於現有最高密鑰），並重置 `Key Rollover Required` 標誌 `DomainServerInfo`。

   1. 對於每個域密鑰，生成域憑據。

該引用實現實現了以下用於域註銷的邏輯：

1. 從請求URL分析域名。
1. 在中查找請求的域名 `DomainServerInfo` 的子菜單。
1. 如果請求的域需要身份驗證，請確保請求中包含有效的身份驗證令牌，並與身份驗證命名空間匹配（如果在資料庫中指定）。
1. 查找中的域名和電腦GUID `DomainMembership` 的子菜單。 如果找不到匹配項，則返回錯誤 `DEREG_DENIED (401)`。

1. 如果這不是預覽請求，請從 `DomainMembership` 並設定 `Key Rollover Required` 標誌 `DomainServerInfo`。

在此使用情況下，由於大量電腦可以加入域，因此無法完全匹配電腦ID。 而是使用在個性化期間分配給電腦的隨機電腦GUID。
