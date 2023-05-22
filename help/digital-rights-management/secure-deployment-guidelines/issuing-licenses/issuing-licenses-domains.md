---
description: 要防止用戶備份和恢復檔案以繞過域註銷，必須實施一些域管理方法。
title: 管理域
exl-id: cbf745d2-ba6e-4144-9608-23870bdfe16d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 管理域 {#managing-domains}

要防止用戶備份和恢復檔案以繞過域註銷，必須實施一些域管理方法。

以下是一些域管理方法：

* 限制域憑據有效的時間。

   客戶端需要與域伺服器聯繫以在憑據過期時重新獲取域憑據。 此時，域伺服器可以驗證電腦是否仍被授權為域的成員。
* 每次用戶註銷時，將滑鼠指針置於域鍵上。

   許可證伺服器應僅向具有最新域密鑰的客戶端頒發許可證。 此方法假定許可證伺服器可以與域伺服器協調以知道哪個密鑰是最新的。 滾動域密鑰涉及為域生成新密鑰對。 滾動到域的鍵時，請在 `generateDomainCredential`。
* 如果域伺服器與許可證伺服器相同，則伺服器可以使用回滾計數器檢測備份和還原。

   有關詳細資訊，請參見 [處理Adobe PrimetimeDRM請求](../../protecting-content/implementing-the-license-server/processing-drm-requests.md)。
