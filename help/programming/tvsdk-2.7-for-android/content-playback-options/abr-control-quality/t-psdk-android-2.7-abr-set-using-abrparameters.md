---
description: 您只能使用ABRControlParameters設定ABR控制值，但您可以隨時建構新的控制值。
title: 使用ABRControlParameters設定最適化位元速率
exl-id: fc7887bd-37e8-48e7-8afb-3946fb3f1e77
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 使用ABRControlParameters設定最適化位元速率 {#configure-adaptive-bit-rates-using-abrcontrolparameters}

您只能使用ABRControlParameters設定ABR控制值，但您可以隨時建構新的控制值。

下列條件適用於 `ABRControlParameters`：

* 在建構時，您必須提供所有引數的值。
* 建構後，您無法變更個別值。
* 如果您指定的引數超出允許的範圍，則 `ArgumentError` 擲回。

1. 決定您的初始、最小和最大位元速率。
1. 確定ABR原則：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 將ABR引數值設定在 `ABRControlParameters` 建構函式並將值指派給媒體播放器。

   ```
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```
