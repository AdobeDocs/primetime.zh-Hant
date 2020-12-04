---
description: 為防止用戶備份和恢復檔案以繞過域取消註冊，您必須實施一些域管理方法。
seo-description: 為防止用戶備份和恢復檔案以繞過域取消註冊，您必須實施一些域管理方法。
seo-title: 管理網域
title: 管理網域
uuid: 30b73e38-d6ed-43c6-89ba-ae8616383779
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# 管理域{#managing-domains}

為防止用戶備份和恢復檔案以繞過域取消註冊，您必須實施一些域管理方法。

以下是一些域管理方法：

* 限制域憑據有效的時間。

   當憑證到期時，用戶端需要連絡網域伺服器以重新取得網域憑證。 此時，域伺服器可以驗證電腦是否仍被授權為域的成員。
* 每次用戶取消註冊時，將滑鼠指針置於域鍵上。

   授權伺服器僅應向擁有最新網域金鑰的用戶端發行授權。 此方法假定許可證伺服器可以與域伺服器協調，以知道哪個密鑰是最新的。 滾動域密鑰涉及為域生成新密鑰對。 當指向域的鍵時，請遞增`generateDomainCredential`中的鍵版本。
* 如果域伺服器與許可證伺服器相同，伺服器可以使用回滾計數器來檢測備份和還原。

   如需詳細資訊，請參閱[處理Adobe Primetime DRM請求](../../protecting-content/implementing-the-license-server/processing-drm-requests.md)。

