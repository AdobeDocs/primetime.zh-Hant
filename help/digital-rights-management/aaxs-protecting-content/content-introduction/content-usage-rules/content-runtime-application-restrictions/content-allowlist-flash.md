---
title: 允許Adobe®Flash®播放器SWF播放受保護內容的清單
description: 允許Adobe®Flash®播放器SWF播放受保護內容的清單
copied-description: true
exl-id: e6adf548-c5d5-45d0-bcd3-ef5185092291
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 允許Adobe®Flash®播放器SWF播放受保護內容的清單 {#allowlist-for-adobe-flash-player-swfs-allowed-to-play-protected-content}

指定可播放內容的SWF檔案。 通過使用SWF內容計算的SWFURL或SHA-256摘要指定SWF檔案。 如果使用SHA-256摘要，此用法規則還指定允許客戶端下載和驗證SWF的最長時間。

示例用例：在Flash Media Server的情況下，概念上等同於「SWF驗證」，但在客戶端強制實施，以限制哪些視頻播放器可以播放內容。 請注意，與父Adobe相比，在強制實施子SWF方面，「SWF訪問」行為不同。
