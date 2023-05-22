---
title: 管理域
description: 管理域
copied-description: true
exl-id: c9030373-fd54-4745-9f03-0218532b9d6d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 管理域{#managing-domains}

為防止用戶能夠備份和恢復其檔案以繞過域註銷，建議對域管理實施以下方法之一：

* 限制域憑據有效的時間。 客戶端需要與域伺服器聯繫以在域憑據過期時重新獲取域憑據。 此時，域伺服器可以確保電腦仍被授權為域的成員。
* 每次用戶取消註冊時都將滑鼠指針置於域密鑰上。 許可證伺服器應僅向具有最新域密鑰的客戶端頒發許可證。 這假定許可證伺服器可以與域伺服器協調以知道哪個密鑰是最新的。 滾動域密鑰涉及為域生成新密鑰對。 滾動特定域的密鑰時，請確保在 `generateDomainCredential`。 有關實施密鑰滾動更新的詳細資訊，請參見 *RefImplDomainReqHandler* 的上界。
* 如果域伺服器與許可證伺服器相同，則伺服器可以使用回滾計數器來檢測備份和恢復。 請參閱*處理Adobe訪問請求*中 *使用Adobe訪問SDK保護內容。*
