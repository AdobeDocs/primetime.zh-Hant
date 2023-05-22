---
title: 打包選項
description: 打包選項
copied-description: true
exl-id: 64c5c22d-0041-4fb9-80d0-72e11cb775f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# 打包選項{#packaging-options}

您可以選擇多種選項來打包內容。 可以在 `DRMParameters` 介面和實現可介麵類。 通過這些類，您可以設定簽名和密鑰參數，並指示是加密音頻內容、視頻內容還是指令碼資料。 要瞭解這些命令在參考實現中是如何實現的，請參閱中討論的「介質打包器」命令行選項的說明 *使用Adobe PrimetimeDRM參考實現*。 這些選項基於Java API，因此可用於寫程式使用。

打包選項包括：

* 加密選項（音頻、視頻、部分加密）。
* 客戶端用作向許可證伺服器發送的所有請求的基本URL的許可證伺服器URL
* 許可證伺服器傳輸證書
* 用於加密CEK的許可證伺服器證書
* 用於對元資料簽名的打包器憑據
