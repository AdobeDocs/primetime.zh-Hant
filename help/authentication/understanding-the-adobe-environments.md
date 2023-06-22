---
title: 瞭解Adobe環境
description: 瞭解Adobe環境
exl-id: bb6cf37f-48cd-47bb-b3c2-f7a96e49b12d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 瞭解Adobe環境 {#understanding-the-adobe-environments}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

推出說明Adobe環境的官方檔案 [在Pre-qual中設定您的環境和測試](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md)：

Adobe環境，概括為幾個字：

Adobe有兩個環境： **資格預審** 和 **版本**.

* 在「資格預審」環境中，我們正在準備要發佈的新版本編號。

* 目前的版本編號在版本環境中。

每個環境都有兩個設定檔： **分段** 和 **生產**.

* 中繼設定檔會連線至MVPD中繼伺服器
* 生產設定檔會連線到MVPD生產設定檔。

擁有這兩個設定檔的原因是，在中繼設定檔上，我們讓新合作夥伴準備上線，他們想要使用即將推出的組建（資格預審）或發行版本（更穩定）來測試系統。

如果合作夥伴想要測試新版本，則需要完成額外的幾個步驟。 請參閱， [在Pre-qual中設定您的環境和測試](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

依照上述步驟操作，即可確保即將發行的版本將會在資格預審環境中進行測試。
