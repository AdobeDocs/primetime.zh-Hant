---
title: 轉碼與標準化
description: 轉碼與標準化
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 轉碼和標準化{#transcoding-and-normalization}

PrimetimeAd Insertion將嘗試比對，以確保內容與廣告的觀看體驗一致：

1. 來源串流轉碼器和位元速率，同時在轉碼時始終選擇最高品質／位元速率創意素材

1. 源流碎片大小(HLS/#EXT-X-TARGETDURATION)

1. 轉碼偏好的創意格式

1. 音訊自動調平功能，以確保所有廣告創意素材的dB層級一致。

>[!NOTE]
>
>由PrimetimeAd Insertion的即時轉碼產生的HLS資產會產生第3版的HLS資產，不論內容中定義了哪個HLS版本。
