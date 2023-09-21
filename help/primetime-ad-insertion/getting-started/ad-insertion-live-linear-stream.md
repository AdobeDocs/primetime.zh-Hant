---
title: 在即時/線性資料流中使用Ad Insertion
description: 在即時/線性資料流中使用Ad Insertion
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 在即時/線性資料流中使用Ad Insertion {#ad-insertion-live-linear-stream}

PrimetimeAd Insertion讓發佈者能夠處理即時/線性串流期間發生的標準和複雜廣告插入情況。

## 支援的提示格式 {#cue-formats-supported}

PrimetimeAd Insertion支援多種標準和非標準提示格式，包括：

* DPI SCTE-35 （SCTE-35增強型廣告標籤）

* [Adobe數位程式插入訊號規格](assets/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* 二進位SCTE-35 （HLS和DASH）

* 文字SCTE-35 （HLS和DASH）

請聯絡您的Primetime支援代表，以取得其他詳細資料或其他支援的提示格式。

## 部分廣告插播支援 {#partial-ad-break-support}

部分廣告插播可用於觀看者在廣告插播開始後進入即時/線性資料流的情況。  例如，如果檢視者在1:00標籤處輸入2:00的廣告插播，則部分廣告插播插入可確保剩餘時間提供廣告。 若未插入部分廣告插播，插播期間不會對此檢視者提供任何廣告。 如果媒體串流中存在適當的標籤，PrimetimeAd Insertion預設會啟用部分廣告插播插入。

## 提早返回（提早廣告退出） {#early-return-early-ad-exit}

在某些情況下，您可能需要從即時/線性資料流的廣告插播中提早返回，例如當體育活動突然返回進行中時。 每個廣告決策格式都包含「cue-out」（廣告）或「cue-in」（內容）的標籤。  如果在廣告插播結束前遇到「提示加入」標籤，Adobe PrimetimeAd Insertion會遵循該提示加入。  請連絡您的內容封裝程式以啟用提早傳回。
