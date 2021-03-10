---
title: 管理網域
description: 管理網域
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 管理域{#managing-domains}

為防止用戶通過略過域取消註冊來備份和恢復其檔案，建議對域管理實施以下方法之一：

* 限制域憑據有效的時間。 客戶端需要聯繫域伺服器，以便在域證書過期時重新獲取域證書。 那時，域伺服器可以確保電腦仍被授權為域的成員。
* 每次用戶取消註冊時都變換域密鑰。 授權伺服器僅應向擁有最新網域金鑰的用戶端發行授權。 這假定許可證伺服器可以與域伺服器協調，以知道哪個密鑰是最新的。 滾動域密鑰涉及為域生成新密鑰對。 滾動到特定域的鍵時，請務必在`generateDomainCredential`中增加鍵版本。 如需實作密鑰變換的詳細資訊，請參閱參考實作中的&#x200B;*RefImplDomainReqHandler*。
* 如果域伺服器與許可證伺服器相同，伺服器可以使用回滾計數器來檢測備份和還原。 請參閱&#x200B;*使用Adobe存取SDK保護內容中的*處理Adobe存取要求*。*

