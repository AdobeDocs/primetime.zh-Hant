---
title: 匿名網域邏輯
description: 匿名網域邏輯
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 匿名域邏輯{#anonymous-domain-logic}

## 域註冊邏輯{#section_C91DCD49D7D44570AF98C2D7B8A283F9}

參考實作適用於匿名網域註冊的下列邏輯：

1. 從請求URL剖析網域名稱。
1. 在`DomainServerInfo`表中查找域名。
1. 如果找不到條目，請在表中插入條目。

   預設值為：

   * `authentication is not required`
   * `no membership maximum`

   如果要求的網域需要驗證，請確定請求中有有效的驗證Token。 如果在資料庫中指定「驗證名稱空間」，則Token必須符合指定的「驗證名稱空間」。
1. 如果需要驗證，但無有效驗證Token，則傳回錯誤`DOM_AUTHENTICATION_REQUIRED (503)`。
1. 檢查設備是否已向域註冊：

   1. 在`DomainMembership`表中查找域名。
   1. 比較您在請求中找到的機器GUID和機器GUID。
   1. 如果這是新機器，請在`DomainMembership`表格中新增項目。
   1. 如果它是新設備，且已達到`Max Membership`值，則返回錯誤`DOM_LIMIT_REACHED (502)`。

1. 在`DomainKeys`表中查找此域的所有域鍵：

   1. 如果`DomainServerInfo`指示需要滾動鍵，則生成新鍵對。
   1. 在`DomainKeys`表中保存密鑰對，其密鑰版本比現有的最高密鑰版本高1個數字。
   1. 重設`DomainServerInfo`中的`Key Rollover Required`標幟。

   1. 對於每個域密鑰，生成域憑據。

## 域取消註冊邏輯{#section_C968BBFCBFAB4510A903D169F38C9FCE}

參考實作適用於匿名網域取消註冊的下列邏輯：

1. 從請求URL剖析網域名稱。
1. 在`DomainServerInfo`表中查找請求的域名。
1. 如果要求的網域需要驗證，請確定請求中有有效的驗證Token。

   此Token也必須符合資料庫中指定的Auth Namespace。
1. 在`DomainMembership`表中查找域名和電腦GUID。

   如果找不到匹配的條目，則返回錯誤`DEREG_DENIED (401)`。

1. 如果這不是預覽請求，請從`DomainMembership`刪除條目，並在`DomainServerInfo`中設定`Key Rollover Required`標籤。

由於許多電腦可能加入域，因此不能簡單地與電腦ID匹配。 而是套用在個人化期間指派給機器的隨機機器GUID。
