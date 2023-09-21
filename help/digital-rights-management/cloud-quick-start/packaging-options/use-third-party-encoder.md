---
title: 使用協力廠商編碼器
description: 使用協力廠商編碼器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 使用協力廠商編碼器{#use-a-third-party-encoder}

有些客戶可能已經擁有使用硬體或軟體視訊編碼器(或Adobe Media Server)的內容準備管道。 如果是這種情況，任何目前可以建立Primetime DRM保護內容的產品都可以使用與Primetime Cloud DRM Protection Kit相同的組態設定，來封裝Primetime Cloud DRM的內容。 所需的資訊可從套件中包含的任何現有組態檔中取得： [!DNL config_hls.xml] 或 [!DNL config_hds.xml].

相關的設定專案包括：

* 授權伺服器URL
* 金鑰伺服器URL
* 授權伺服器憑證
* 傳輸憑證
