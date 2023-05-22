---
description: TVSDK下載廣告段並在設備螢幕上呈現這些廣告段。
title: 廣告播放階段
exl-id: c12dcf84-0daa-4bc2-8e17-fdf47a760296
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 廣告播放階段{#ad-playback-phase}

TVSDK下載廣告段並在設備螢幕上呈現這些廣告段。

此時，TVSDK已解析廣告，將其定位到時間軸上，並嘗試在螢幕上呈現內容。

此階段可能出現以下主要錯誤類別：

* 連接到主機伺服器時出錯
* 下載清單檔案時出錯
* 下載媒體段時出錯

對於所有三個錯誤類，TVSDK會將觸發的事件轉發到您的應用程式，包括：

* 故障轉移時觸發的通知事件。
* 配置檔案因故障轉移算法而更改時的通知事件。
* 當已考慮所有故障轉移選項且無法自動執行其他操作時觸發的通知事件。

   您的應用程式需要採取相應的操作。

無論是否發生錯誤，TVSDK都會為每個錯誤調用onAdBreakComplete `onAdBreakStart` 和 `onAdComplete` 每 `onAdStart`。 但是，如果無法下載段，則時間線中可能存在間隙。 當間隙足夠大時，播放頭位置值和所報告的廣告進度值可能會出現不連續。
