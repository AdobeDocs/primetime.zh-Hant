---
description: 為防止用戶備份和恢復檔案以繞過域取消註冊，您必須實施一些域管理方法。
title: 管理網域
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# 管理域{#managing-domains}

為防止用戶備份和恢復檔案以繞過域取消註冊，您必須實施一些域管理方法。

以下是一些域管理方法：

* 限制域憑據有效的時間。

   當憑證到期時，用戶端需要連絡網域伺服器以重新取得網域憑證。 此時，域伺服器可以驗證電腦是否仍被授權為域的成員。
* 每次用戶取消註冊時，將滑鼠指針置於域鍵上。

   授權伺服器僅應向擁有最新網域金鑰的用戶端發行授權。 此方法假定許可證伺服器可以與域伺服器協調，以知道哪個密鑰是最新的。 滾動域密鑰涉及為域生成新密鑰對。 將滑鼠指針置於域的鍵上時，請遞增`generateDomainCredential`中的鍵版本。
* 如果域伺服器與許可證伺服器相同，伺服器可以使用回滾計數器來檢測備份和還原。

   如需詳細資訊，請參閱「處理Adobe PrimetimeDRM請求」](../../protecting-content/implementing-the-license-server/processing-drm-requests.md)。[

