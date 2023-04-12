---
title: 了解Adobe環境
description: 了解Adobe環境
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 了解Adobe環境 {#understanding-the-adobe-environments}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

提供說明Adobe環境的官方檔案 [在Pre-qual中設定環境和測試](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md):

Adobe環境，概括為幾個字：

Adobe有兩個環境： **資格預審** 和 **發行**.

* 在資格預審環境中，我們準備要發行的新版本編號。

* 目前的版本編號是在版本環境上。

每個環境有兩個設定檔： **中繼** 和 **生產**.

* 中繼設定檔會連線至MVPD中繼伺服器
* 生產設定檔會連線至MVPD生產設定檔。

有兩個設定檔的原因是，在測試設定檔中，我們準備讓新合作夥伴上線，而他們想要使用即將推出的組建（資格預審）或發行版本（更穩定）來測試系統。

如果合作夥伴想要測試新版本，則需要執行幾項其他步驟。 看， [在Pre-qual中設定環境和測試](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

依照上述步驟操作，即可確保即將發行的版本將在資格預審環境中測試。
