---
title: 管理網域
description: 管理網域
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 管理網域{#managing-domains}

為了防止使用者為了略過網域解除註冊而備份及還原其檔案，建議針對網域管理實作下列其中一種方法：

* 限制網域認證的有效時間長度。 使用者端需要連絡網域伺服器，才能在網域憑證過期時重新取得網域憑證。 屆時，網域伺服器可確保電腦仍獲授權成為網域的成員。
* 每次使用者取消註冊時，將網域金鑰滑鼠指向上方。 授權伺服器應該只向擁有最新網域金鑰的使用者端發行授權。 這假設授權伺服器可以和網域伺服器協調以知道哪個金鑰是最新的金鑰。 捲動網域金鑰涉及為網域產生新的金鑰組。 將滑鼠指向特定網域的金鑰時，請務必增加中的金鑰版本 `generateDomainCredential`. 如需實作金鑰變換的詳細資訊，請參閱 *RefImplDomainReqHandler* 在參考實作中。
* 如果網域伺服器與授權伺服器相同，伺服器可以使用復原計數器來偵測備份和還原。 請參閱*中的*處理Adobe存取要求* *使用Adobe存取SDK來保護內容。*
