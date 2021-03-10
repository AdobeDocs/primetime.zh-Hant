---
title: 使用協力廠商編碼器
description: 使用協力廠商編碼器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 使用協力廠商編碼器{#use-a-third-party-encoder}

有些客戶可能已使用硬體或軟體視訊編碼器(或Adobe Medium伺服器)準備內容。 如果是這樣，任何目前可建立受Primetime DRM保護內容的產品，都可使用與Primetime Cloud DRM保護套件相同的組態設定來封裝Primetime Cloud DRM的內容。 所需資訊可從工具包中包含的任何現有配置檔案中獲取：[!DNL config_hls.xml]或[!DNL config_hds.xml]。

相關配置項目為：

* 授權伺服器URL
* 關鍵伺服器URL
* 授權伺服器憑證
* 傳輸憑證

