---
description: 若要防止使用者備份及還原檔案以略過網域取消註冊，您必須實作一些網域管理方法。
title: 管理網域
exl-id: cbf745d2-ba6e-4144-9608-23870bdfe16d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 管理網域 {#managing-domains}

若要防止使用者備份及還原檔案以略過網域取消註冊，您必須實作一些網域管理方法。

以下是一些網域管理方法：

* 限制網域認證的有效時間長度。

   使用者端需要連絡網域伺服器，才能在認證過期時重新取得網域認證。 屆時，網域伺服器可確認電腦仍獲授權成為網域的成員。
* 每次使用者取消註冊時，將滑鼠移到網域金鑰上。

   License Server應該只向擁有最新網域金鑰的使用者端發行授權。 此方法假設License Server可以與Domain Server協調，知道哪個金鑰是最新的。 捲動網域金鑰涉及為網域產生新的金鑰組。 將滑鼠指向某個網域的金鑰時，請將金鑰版本增加為 `generateDomainCredential`.
* 如果網域伺服器與License Server相同，則伺服器可以使用復原計數器來偵測備份和還原。

   如需詳細資訊，請參閱 [處理Adobe Primetime DRM請求](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).
