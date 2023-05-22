---
description: 如果您的系統可以訪問硬體輔助解碼，則與使用iFrame格式的純軟體TVSDK實現相比，您可以實現更流暢的特技播放。
title: 更流暢的特技播放操作
exl-id: f69bf480-122b-474d-8f35-31655ea87c70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 更流暢的特技播放操作 {#smoother-trick-play-operations}

如果您的系統可以訪問硬體輔助解碼，則與使用iFrame格式的純軟體TVSDK實現相比，您可以實現更流暢的特技播放。

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

使用iFrame格式會導致特技播放操作不平滑。 更平滑的特技播放操作使用正常（而非iFrame）配置檔案、硬體解碼支援和增加的幀速率。 不同的硬體輔助解碼設備具有不同的能力。 雙倍速度要求每秒60幀(FPS)，而四倍速度要求120 FPS。

>[!IMPORTANT]
>
>Adobe建議將較新Android設備的播放速度限制為兩倍，而不要對較舊的Android設備使用該功能。

要實現更流暢的特技播放，請設定 `ABRControlParameters.maxPlayoutRate` 達到所需的正常速度倍數（例如，2.0表示雙速度）。 如果後續呼叫 `MediaPlayer.setRate()` 參數小於或等於為設定的值 `maxPlayoutRate`, TVSDK使用常規配置檔案來實現更平滑的特技播放。 否則，它將使用iFrame配置檔案進行滴答操作。
