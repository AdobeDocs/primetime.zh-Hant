---
description: 若要防止使用者備份和還原檔案以略過網域取消註冊，您必須實作一些網域管理方法。
title: 管理網域
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 管理網域 {#managing-domains}

若要防止使用者備份和還原檔案以略過網域取消註冊，您必須實作一些網域管理方法。

以下是一些網域管理方法：

* 限制網域認證的有效時間長度。

  使用者端需要連絡網域伺服器，才能在認證過期時重新取得網域認證。 屆時，網域伺服器可確認電腦仍獲授權成為網域成員。
* 每次使用者取消註冊時，將滑鼠移到網域金鑰上。

  授權伺服器應該只向擁有最新網域金鑰的使用者端發行授權。 這個方法假設許可證伺服器可以和領域伺服器協調以知道哪個金鑰是最新的金鑰。 捲動網域金鑰涉及為網域產生新的金鑰組。 將滑鼠指向網域的金鑰時，增加中的金鑰版本 `generateDomainCredential`.
* 如果網域伺服器與授權伺服器相同，伺服器可以使用復原計數器來偵測備份和還原。

  如需詳細資訊，請參閱 [處理Adobe Primetime DRM請求](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).
