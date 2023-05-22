---
title: 使用第三方編碼器
description: 使用第三方編碼器
copied-description: true
exl-id: 565f69db-8595-4f78-b1e6-26f277a3784a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 使用第三方編碼器{#use-a-third-party-encoder}

有些客戶可能已使用硬體或軟體視頻編碼器(或Adobe Medium伺服器)準備了內容準備管道。 如果是這樣，任何當前可以建立黃金時段DRM保護內容的產品都可以使用與黃金時段雲DRM保護套件相同的配置設定來為黃金時段雲DRM打包內容。 可從套件中包含的任何現有配置檔案獲取所需資訊： [!DNL config_hls.xml] 或 [!DNL config_hds.xml]。

相關配置項目為：

* 許可證伺服器URL
* 密鑰伺服器URL
* 許可證伺服器證書
* 傳輸證書
