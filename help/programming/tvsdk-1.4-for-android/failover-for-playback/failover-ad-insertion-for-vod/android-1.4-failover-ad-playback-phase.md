---
description: TVSDK會下載廣告區段並在裝置的畫面上轉譯它們。
title: 廣告播放階段
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 廣告播放階段{#ad-playback-phase}

TVSDK會下載廣告區段並在裝置的畫面上轉譯它們。

此時，TVSDK已解析廣告、將其定位在時間軸上，並嘗試在畫面上轉譯內容。

此階段可能會發生下列主要錯誤類別：

* 連線到主機伺服器時發生錯誤
* 下載資訊清單檔案時發生錯誤
* 下載媒體區段時發生錯誤

對於全部三個錯誤類別，TVSDK會將觸發的事件轉送至您的應用程式，包括：

* 容錯移轉發生時觸發的通知事件。
* 當設定檔因容錯移轉演演算法而變更時的通知事件。
* 已考慮所有容錯移轉選項時觸發的通知事件，且無法自動採取其他動作。

  您的應用程式需要採取適當的動作。

無論是否發生錯誤，TVSDK都會針對每個呼叫onAdBreakComplete `onAdBreakStart` 和 `onAdComplete` 代表每 `onAdStart`. 但是，如果區段無法下載，則時間表可能會出現間隙。 當間隙夠大時，播放點位置和報告的廣告進度中的值可能會顯示不連續。
