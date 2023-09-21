---
title: 轉碼和標準化
description: 轉碼和標準化
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 轉碼和標準化 {#transcoding-and-normalization}

PrimetimeAd Insertion會嘗試比對以下內容，以確保跨內容和廣告有一致的檢視體驗：

1. 來源資料流轉碼器和位元速率，同時在轉碼時一律選擇最高品質/位元速率創意

1. 來源串流片段大小(HLS/#EXT-X-TARGETDURATION)

1. 轉碼時首選的創意格式

1. 音訊自動平準，確保所有廣告創意內容都具備一致的dB層級。

>[!NOTE]
>
>PrimetimeAd Insertion即時轉碼產生的HLS資產會產生版本3的HLS資產，無論內容中定義了哪個HLS版本。
