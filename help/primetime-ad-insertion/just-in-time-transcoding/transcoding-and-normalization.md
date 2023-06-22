---
title: 轉碼和標準化
description: 轉碼和標準化
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 轉碼和標準化 {#transcoding-and-normalization}

PrimetimeAd Insertion會嘗試比對以下內容，以確保跨內容和廣告有一致的檢視體驗：

1. 來源資料流轉碼器和位元速率，同時在轉碼時一律選擇最高品質/位元速率創意

1. 來源資料流片段大小(HLS/#EXT-X-TARGETDURATION)

1. 轉碼時首選的創意格式

1. 音訊自動平準以確保所有廣告創意內容都有一致的dB等級。

>[!NOTE]
>
>PrimetimeAd Insertion產生的HLS資產會即時轉碼產生版本3的HLS資產，無論內容中定義了哪個HLS版本。
