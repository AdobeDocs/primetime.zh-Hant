---
seo-title: 封裝選項
title: 封裝選項
uuid: 04244428-cb42-438a-8f16-91532c70ea60
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# 封裝選項{#packaging-options}

您有許多選項可用來封裝內容。 您可以在`DRMParameters`介面中指定選項，並實現可介面的類。 您可以透過這些類別來設定簽名和金鑰參數，並指出要加密音訊內容、視訊內容或指令碼資料。 若要瞭解這些功能如何在參考實作中實作，請參閱&#x200B;*使用Adobe Primetime DRM參考實作*&#x200B;中討論的Media Packager命令列選項說明。 這些選項是以Java API為基礎，因此可供程式化使用。

封裝選項包括：

* 加密選項（音訊、視訊、部分加密）。
* 用戶端用作傳送至授權伺服器之所有請求之基本URL的授權伺服器URL
* 授權伺服器傳輸憑證
* 用於加密CEK的許可證伺服器證書
* 簽署中繼資料的Packager憑證

