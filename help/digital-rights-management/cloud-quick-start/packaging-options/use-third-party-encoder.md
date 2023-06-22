---
title: 使用協力廠商編碼器
description: 使用協力廠商編碼器
copied-description: true
exl-id: 565f69db-8595-4f78-b1e6-26f277a3784a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 使用協力廠商編碼器{#use-a-third-party-encoder}

有些客戶可能已經使用硬體或軟體視訊編碼器(或Adobe Medium伺服器)進行內容準備。 如果是這種情況，任何目前可以建立Primetime DRM保護內容的產品，都可以使用與Primetime Cloud DRM Protection Kit相同的組態設定，封裝Primetime Cloud DRM的內容。 所需資訊可從套件中包含的任何現有組態檔中取得： [!DNL config_hls.xml] 或 [!DNL config_hds.xml].

相關設定專案包括：

* 授權伺服器URL
* 金鑰伺服器URL
* 授權伺服器憑證
* 傳輸憑證
