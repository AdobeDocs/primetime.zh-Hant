---
description: 如果您的系統可存取硬體輔助解碼，則使用iFrame格式即可獲得比使用純軟體TVSDK實作更流暢的特技播放。
title: 更流暢的魔術戲法操作
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 更流暢的魔術戲法操作 {#smoother-trick-play-operations}

如果您的系統可存取硬體輔助解碼，則使用iFrame格式即可獲得比使用純軟體TVSDK實作更流暢的特技播放。

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

使用iFrame格式會導致特技播放操作不平滑。 更流暢的特技播放作業使用一般（非iFrame）設定檔、硬體解碼支援以及增加的影格速率。 不同的硬體輔助解碼裝置具有不同的功能。 雙速需要每秒60個畫面(FPS)，四速則需要120 FPS。

>[!IMPORTANT]
>
>Adobe建議您將較新Android裝置的播放速度限製為雙倍，而不要將功能用於較舊的Android裝置。

若要獲得更流暢的技巧，請設定 `ABRControlParameters.maxPlayoutRate` 正常速度的所需倍數（例如，雙速為2.0）。 如果後續呼叫 `MediaPlayer.setRate()` 有一個引數小於或等於您設定的值 `maxPlayoutRate`，TVSDK會使用一般設定檔來達到更流暢的特技播放。 否則，它會使用iFrame設定檔進行點選播放作業。
