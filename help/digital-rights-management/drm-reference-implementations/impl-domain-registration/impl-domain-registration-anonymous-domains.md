---
description: 'null'
seo-description: 'null'
seo-title: 匿名網域邏輯
title: 匿名網域邏輯
uuid: bd0e8e51-27dc-4ccf-b285-a80c2ab9e260
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 匿名網域邏輯{#anonymous-domain-logic}

## 域註冊邏輯 {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

參考實作適用於匿名網域註冊的下列邏輯：

1. 從請求URL剖析網域名稱。
1. 在表格中查找域 `DomainServerInfo` 名。
1. 如果找不到條目，請在表中插入條目。

   預設值為：

   * `authentication is not required`
   * `no membership maximum`
   如果要求的網域需要驗證，請確定請求中有有效的驗證Token。 如果在資料庫中指定「驗證名稱空間」，則Token必須符合指定的「驗證名稱空間」。
1. 如果需要驗證，但無有效驗證Token，則傳回錯誤 `DOM_AUTHENTICATION_REQUIRED (503)`。
1. 檢查設備是否已向域註冊：

   1. 在表格中查找域 `DomainMembership` 名。
   1. 比較您在請求中找到的機器GUID和機器GUID。
   1. 如果這是新機器，請在表格中新增項 `DomainMembership` 目。
   1. 如果是新裝置且已 `Max Membership` 到達值，則返回錯誤 `DOM_LIMIT_REACHED (502)`。

1. 在表中查找此域的所有域 `DomainKeys` 鍵：

   1. 如果 `DomainServerInfo` 指出需要轉換密鑰，請生成新密鑰對。
   1. 將鍵對保存在表 `DomainKeys` 中，其密鑰版本高於現有最高密鑰的一個數字。
   1. 在中重 `Key Rollover Required` 設標幟 `DomainServerInfo`。

   1. 對於每個域密鑰，生成域憑據。

## 域取消註冊邏輯 {#section_C968BBFCBFAB4510A903D169F38C9FCE}

參考實作適用於匿名網域取消註冊的下列邏輯：

1. 從請求URL剖析網域名稱。
1. 在表格中查找請求的域 `DomainServerInfo` 名。
1. 如果要求的網域需要驗證，請確定請求中有有效的驗證Token。

   此Token也必須符合資料庫中指定的Auth Namespace。
1. 在表格中查找域名和電腦GUID `DomainMembership` 。

   如果找不到匹配的條目，則返回錯誤 `DEREG_DENIED (401)`。

1. 如果這不是預覽請求，請從中刪除該條 `DomainMembership`目，並在中 `DomainServerInfo`設定標 `Key Rollover Required` 記。

由於許多電腦可能加入域，因此不能簡單地與電腦ID匹配。 而是套用在個人化期間指派給機器的隨機機器GUID。
