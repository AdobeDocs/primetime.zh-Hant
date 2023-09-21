---
title: 關於適用於受保護串流的Adobe Access Server
description: 關於適用於受保護串流的Adobe Access Server
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 關於適用於受保護串流的Adobe Access Server{#about-adobe-access-server-for-protected-streaming}

適用於受保護串流的Adobe® Access™ Server是以Adobe存取SDK為基礎的授權伺服器實作。 此伺服器會發行受保護內容的授權給Adobe存取使用者端。

適用於受保護串流的Adobe Access Server支援多個租使用者，這表示可以代表多個內容發佈者來託管單一伺服器，而每個發佈者都有自己的組態設定。 此外，伺服器支援自訂授權元件，以便在發行授權之前執行自訂邏輯。

此伺服器旨在搭配HTTP資料流使用。 因此，此伺服器實作不支援Adobe存取中可用的所有功能。 例如，適用於受保護串流的Adobe Access Server不支援使用者驗證請求、多項原則、網域繫結授權、授權鏈結或同步處理訊息。
