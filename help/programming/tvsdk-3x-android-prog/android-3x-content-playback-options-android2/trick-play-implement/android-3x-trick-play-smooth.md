---
description: 如果您的系統可存取硬體輔助解碼，則使用iFrame格式即可比使用純軟體TVSDK實作更流暢地玩特技。
title: 更流暢的戲法操作
exl-id: f69bf480-122b-474d-8f35-31655ea87c70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 更流暢的戲法操作 {#smoother-trick-play-operations}

如果您的系統可存取硬體輔助解碼，則使用iFrame格式即可比使用純軟體TVSDK實作更流暢地玩特技。

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

使用iFrame格式會導致特技播放操作不平滑。 更流暢的特技播放操作使用一般（非iFrame）設定檔、硬體解碼支援以及增加的影格速率。 不同的硬體輔助解碼裝置有不同的功能。 雙倍速度需要每秒60個畫面(FPS)，四倍速度需要120 FPS。

>[!IMPORTANT]
>
>Adobe建議您將較新Android裝置的播放速度限製為兩倍，不要在較舊Android裝置上使用功能。

若要獲得更流暢的戲法播放，請設定 `ABRControlParameters.maxPlayoutRate` 至所需的正常速度倍數（例如，雙倍速度為2.0）。 如果後續呼叫 `MediaPlayer.setRate()` 引數小於或等於您設定的值 `maxPlayoutRate`，TVSDK會使用一般設定檔來達到更流暢的戲法播放。 否則，它會使用iFrame設定檔來執行點進作業。
