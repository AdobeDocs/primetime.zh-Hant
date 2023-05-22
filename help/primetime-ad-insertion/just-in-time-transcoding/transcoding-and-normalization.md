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

黃金時段Ad Insertion將嘗試匹配以下內容和廣告，以確保內容和廣告的觀看體驗一致：

1. 源流編解碼器和比特率，同時在轉碼時始終選擇最高質量/比特率

1. 源流碎片大小(HLS/#EXT-X-TARGETDURATION)

1. 用於轉碼的首選創意格式

1. 音頻自動調平，確保所有廣告創意的dB級別一致。

>[!NOTE]
>
>黃金時段Ad Insertion即時轉碼生成的HLS資產將生成版本3的HLS資產，而不管內容中定義了哪個HLS版本。
