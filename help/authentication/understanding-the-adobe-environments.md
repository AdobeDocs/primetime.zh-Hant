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
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

提供了描述Adobe環境的正式檔案 [設定環境並在預定時間內進行測試](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md):

Adobe環境，用幾個詞來總結：

Adobe有兩個環境： **資格預審** 和 **發佈**。

* 在資格預審環境中，我們準備發佈新版本。

* 當前版本生成位於版本環境上。

每個環境有兩個配置檔案： **暫存** 和 **生產**。

* 臨時配置檔案連接到MVPD臨時伺服器
* 生產配置檔案連接到MVPD生產配置檔案。

擁有兩個配置檔案的原因是，在試運行配置檔案中，我們正在準備新合作夥伴投入使用，他們希望將系統與即將構建（資格預審）或發行版test（更穩定）。

如果合作夥伴想要test新版本，則需要執行幾項附加步驟。 看， [設定環境並在預定時間內進行測試](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md)。

通過執行上述步驟，可以確保即將發佈的產品將在資格預審環境中進行測試。
