---
description: TVSDK會下載廣告區段，並在裝置螢幕上呈現廣告區段。
title: 廣告播放階段
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 廣告播放階段{#ad-playback-phase}

TVSDK會下載廣告區段，並在裝置螢幕上呈現廣告區段。

目前，TVSDK已解析廣告、將廣告放在時間軸上，並嘗試在螢幕上呈現內容。

在此階段中可能會出現以下主要錯誤類：

* 連接到主機伺服器時出錯
* 下載資訊清單檔案時發生錯誤
* 下載媒體區段時發生錯誤

對於這三個錯誤類別，TVSDK會將觸發的事件轉送至您的應用程式，包括：

* 發生故障切換時觸發的通知事件。
* 當由於故障切換演算法而變更描述檔時，通知事件。
* 當已考慮所有故障切換選項時觸發的通知事件，且無法自動採取其他操作。

   您的應用程式需要採取適當的動作。

不論是否發生錯誤，TVSDK都會針對每個`onAdBreakStart`和`onAdComplete`呼叫onAdBreakComplete。 `onAdStart`不過，如果無法下載區段，時間軸中可能會有空隙。 當間隙足夠大時，播放磁頭位置中的值和報告的廣告進度可能會出現不連續。
