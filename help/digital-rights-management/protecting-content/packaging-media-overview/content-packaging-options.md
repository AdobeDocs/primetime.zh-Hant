---
title: 封裝選項
description: 封裝選項
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# 封裝選項{#packaging-options}

您有許多選項可用來封裝內容。 您可以在`DRMParameters`介面中指定選項，並實現可介面的類。 您可以透過這些類別來設定簽名和金鑰參數，並指出要加密音訊內容、視訊內容或指令碼資料。 要查看這些命令如何在參考實施中實現，請參閱&#x200B;*使用Adobe PrimetimeDRM參考實施*&#x200B;中討論的Media Packager命令行選項說明。 這些選項是以Java API為基礎，因此可供程式化使用。

封裝選項包括：

* 加密選項（音訊、視訊、部分加密）。
* 用戶端用作傳送至授權伺服器之所有請求之基本URL的授權伺服器URL
* 授權伺服器傳輸憑證
* 用於加密CEK的許可證伺服器證書
* 簽署中繼資料的Packager憑證

