---
title: 在即時／線性串流中使用廣告插入
description: 在即時／線性串流中使用廣告插入
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# 在即時／線性串流{#ad-insertion-live-linear-stream}中使用廣告插入

Primetime廣告插入可讓發佈者處理即時／線性串流期間發生的標準和複雜廣告插入情形。

## 支援的Cue格式{#cue-formats-supported}

Primetime廣告插入支援多種標準和非標準提示格式，包括：

* DPI SCTE-35（SCTE-35增強廣告標籤）

* [Adobe數位程式插入訊號規格](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* 二進位SCTE-35（HLS和DASH）

* 文本SCTE-35（HLS和DASH）

請連絡您的Primetime支援代表，以取得詳細資訊或其他支援的提示格式。

## 部分廣告插播支援{#partial-ad-break-support}

部分廣告插播可用於檢視器在廣告插播開始後進入即時／線性串流的情況。  例如，如果檢視器在1:00的標籤上輸入2:00的長廣告插播，則部分廣告插播可確保廣告在剩餘的時間內提供。 若未插入部分廣告插頁，則在插頁期間不會向此檢視器提供廣告。 如果媒體串流中有適當的標籤，則Primetime廣告插入預設會啟用部分廣告插播。

## 提早退貨（提前廣告退出）{#early-return-early-ad-exit}

有時可能需要從即時／線性串流中的廣告插播提早返回，例如當體育賽事突然返回行動時。 每種廣告決策格式都包含一個標籤，標籤為「提示」（廣告）或「提示」（內容）。  如果在廣告插播結束前遇到「提示」標籤，Adobe Primetime廣告插入將會遵守提示。  請連絡您的內容封裝工具，以啟用提早回傳。
