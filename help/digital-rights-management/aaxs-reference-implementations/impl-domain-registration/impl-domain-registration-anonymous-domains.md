---
seo-title: 匿名網域
title: 匿名網域
uuid: ee29ae4d-65b2-48de-b441-18c8cf55de32
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# 匿名網域 {#anonymous-domains}

在此使用案例中，大量裝置屬於單一網域，因此可能不需要驗證。 要將此類型的域與參考實施一起使用，請建立指定需要域註冊的策略。 指定網域伺服器URL為 `https:// host:port/flashaccess/domainserver/domainname/` 並指定匿名驗證。

參考實現實現了以下域註冊邏輯：

1. 從請求URL剖析網域名稱。
1. 查閱表格中的網域 `DomainServerInfo` 名稱。 如果找不到條目，請將條目插入表中(預設值：驗證不是必需的，而且沒有最大會員資格)。
1. 如果請求的網域需要驗證，請確定請求中包含有效的驗證Token，並符合「驗證名稱空間」（如果在資料庫中指定）。

   1. 如果需要驗證但未提供有效驗證Token，則傳回錯誤 `DOM_AUTHENTICATION_REQUIRED (503)`。

1. 檢查設備是否已向域註冊：

   1. 查閱表格中的網域 `DomainMembership` 名稱。 對於找到的每台電腦GUID，請與請求中的電腦GUID進行比較。 如果這是新機器，請將條目添加到表 `DomainMembership` 中。

   1. 如果是新裝置，且已達到最大會籍，則傳回錯誤 `DOM_LIMIT_REACHED (502)`。

1. 在表格中查閱此網域的所有網域 `DomainKeys` 索引鍵。

   1. 如果 `DomainServerInfo` 指出需要轉換密鑰，請生成新的密鑰對，將其保存在表中 `DomainKeys` （密鑰版本比現有的最高密鑰高1），並重置 `Key Rollover Required` 中的標籤 `DomainServerInfo`。

   1. 對於每個域密鑰，生成域憑據。

該參考實現實現了以下用於域取消註冊的邏輯：

1. 從請求URL剖析網域名稱。
1. 在表格中查閱請求的網 `DomainServerInfo` 域名。
1. 如果請求的網域需要驗證，請確定請求中包含有效的驗證Token，並符合「驗證名稱空間」（如果在資料庫中指定）。
1. 在表格中查閱網域名稱和機器 `DomainMembership` GUID。 如果找不到相符的項目，則返回錯誤 `DEREG_DENIED (401)`。

1. 如果這不是預覽請求，請從中刪除該條目， `DomainMembership` 並在中 `Key Rollover Required` 設定標幟 `DomainServerInfo`。

在此使用案例中，由於許多電腦可以加入域，因此無法完全匹配電腦ID。 而是使用在個人化期間指派給機器的隨機機器GUID。
