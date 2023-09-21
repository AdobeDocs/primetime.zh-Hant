---
title: 封裝選項
description: 封裝選項
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# 封裝選項{#packaging-options}

封裝內容有多種選項。 您可以在 `DRMParameters` 介面並實作可以介面的類別。 使用這些類別，您可以設定簽名和金鑰引數，以及指示是否要加密音訊內容、視訊內容或指令碼資料。 若要檢視如何在參考實作中實作這些專案，請參閱中討論的「媒體封裝器」命令列選項說明 *使用Adobe Primetime DRM參考實作*. 這些選項是以Java API為基礎，因此可在程式設計中使用。

封裝選項包括：

* 加密選項（音訊、視訊、部分加密）。
* 使用者端用作傳送至授權伺服器之所有要求的基底URL的授權伺服器URL
* 授權伺服器傳輸憑證
* 授權伺服器憑證，用於加密CEK
* 用於簽署中繼資料的封裝程式認證
