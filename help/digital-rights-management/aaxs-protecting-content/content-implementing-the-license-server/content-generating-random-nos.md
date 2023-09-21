---
title: 產生隨機數字
description: 產生隨機數字
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# 產生隨機數字{#generating-random-numbers}

Linux伺服器上可使用硬體隨機數字產生器，以確保產生足夠的平均資訊量。 如果電腦無法產生足夠的平均資訊量，在等待來自的資料時，需要隨機來源的Adobe存取操作將會封鎖 `/dev/random`.
