---
title: 在即時/線性資料流中使用Ad Insertion
description: 在即時/線性資料流中使用Ad Insertion
exl-id: d56ed723-ec72-4bbd-befc-6858c7c9d800
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 在即時/線性資料流中使用Ad Insertion {#ad-insertion-live-linear-stream}

PrimetimeAd Insertion可讓發佈者處理在即時/線性串流期間發生的標準和複雜廣告插入情況。

## 支援的提示格式 {#cue-formats-supported}

PrimetimeAd Insertion支援各種標準和非標準提示格式，包括：

* DPI SCTE-35 （SCTE-35增強型廣告標籤）

* [Adobe數位程式插入訊號規格](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* 二進位SCTE-35 （HLS和DASH）

* 文字SCTE-35 （HLS和DASH）

如需其他詳細資訊或其他支援的提示格式，請聯絡您的Primetime支援代表。

## 部分廣告插播支援 {#partial-ad-break-support}

部分廣告插播可用於觀看者在廣告插播開始後進入即時/線性資料流的情況。  例如，如果檢視者在1:00標籤處輸入2:00的廣告插播，則部分廣告插播可確保將在剩餘時間提供廣告。 如果沒有插入部分廣告插播，插播期間將不會對此檢視者提供任何廣告。 如果媒體串流中存在適當的標籤，PrimetimeAd Insertion會預設啟用部分廣告插播插入。

## 提早回訪（提前廣告退出） {#early-return-early-ad-exit}

在某些情況下，您可能需要從即時/線性資料流的廣告插播中提早返回，例如當體育賽事突然恢復運作時。 每個廣告決策格式都包含「提示」（廣告）或「提示」（內容）的標籤。  如果在廣告插播結束前遇到「提示加入」標籤，Adobe PrimetimeAd Insertion會依照該提示加入。  請聯絡您的內容封裝程式以啟用提早傳回。
