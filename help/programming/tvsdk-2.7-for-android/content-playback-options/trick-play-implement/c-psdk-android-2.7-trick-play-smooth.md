---
description: 如果您的系統可存取硬體輔助解碼，則可比使用iFrame格式的純軟體TVSDK實作更順暢的特技播放。
seo-description: 如果您的系統可存取硬體輔助解碼，則可比使用iFrame格式的純軟體TVSDK實作更順暢的特技播放。
seo-title: 更順暢的特技播放作業
title: 更順暢的特技播放作業
uuid: 4749bfa0-17bf-4444-a167-987249945325
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 更順暢的特技播放作業 {#smoother-trick-play-operations}

如果您的系統可存取硬體輔助解碼，則可比使用iFrame格式的純軟體TVSDK實作更順暢的特技播放。

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

使用iFrame格式會產生不順暢的特技播放作業。 更順暢的特技播放作業使用一般（而非iFrame）描述檔、硬體解碼支援和增加的影格速率。 不同的硬體輔助解碼設備具有不同的效能。 雙倍速度需要每秒60幀(FPS)，而四倍速度需要120 FPS。

>[!IMPORTANT]
>
>Adobe建議您針對較新的Android裝置將播放速度限制為兩倍，而不要針對較舊的Android裝置使用此功能。

若要更順暢地播放特技 `ABRControlParameters.maxPlayoutRate` 節目，請設定為所需的正常速度倍數（例如，雙速度為2.0）。 如果後續呼叫 `MediaPlayer.setRate()` 的引數小於或等於您設定的值 `maxPlayoutRate`,TVSDK會使用一般描述檔來產生更順暢的特技播放。 否則，它會使用iFrame描述檔進行滴答作業。
