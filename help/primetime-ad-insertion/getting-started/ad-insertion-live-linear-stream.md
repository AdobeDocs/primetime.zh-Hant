---
title: 在即時/線性流中使用Ad Insertion
description: 在即時/線性流中使用Ad Insertion
exl-id: d56ed723-ec72-4bbd-befc-6858c7c9d800
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 在即時/線性流中使用Ad Insertion {#ad-insertion-live-linear-stream}

黃金時段Ad Insertion使出版商能夠處理即時/線性流期間出現的標準和複雜的廣告插入情況。

## 支援的提示格式 {#cue-formats-supported}

黃金時段Ad Insertion支援多種標準和非標準提示格式，包括：

* DPI SCTE-35（SCTE-35增強標籤）

* [Adobe數字程式插入信令規範](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* 二進位SCTE-35（HLS和DASH）

* 文本SCTE-35（HLS和DASH）

請與您的Mighi時支援代表聯繫，以獲取更多詳細資訊或其他支援的提示格式。

## 部分廣告中斷支援 {#partial-ad-break-support}

在廣告中斷開始後觀看者進入即時/線性流的情況下，可以使用部分廣告中斷。  例如，如果觀眾在1:00標籤處輸入2:00的長廣告分段，則部分廣告分段插入可確保廣告在剩餘時間內投放。 如果不插入部分廣告片段，則在中斷期間不會向此查看器提供廣告。 如果媒體流中存在適當的標籤，則黃金時段Ad Insertion預設啟用部分廣告分段插入。

## 早退（早退） {#early-return-early-ad-exit}

有些情況下，可能需要從即時/線性流中的廣告中斷中提前返回，例如當體育賽事突然恢復活動時。 每個廣告決策格式都包含一個標籤，用於「提示輸出」（廣告）或「提示輸入」（內容）。  如果在廣告中斷結束前遇到「提示」標籤，Adobe PrimetimeAd Insertion將遵守提示。  請與內容打包員聯繫以啟用早退。
