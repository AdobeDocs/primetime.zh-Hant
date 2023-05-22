---
description: 您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新的控制值。
title: 使用ABRControlParameters配置自適應比特率
exl-id: 1f8a4a97-0341-43e7-afdf-801275bc8c94
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 使用ABRControlParameters配置自適應比特率 {#configure-adaptive-bit-rates-using-abrcontrolparameters}

您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新的控制值。

以下條件適用於 `ABRControlParameters`:

* 在構造時，必須提供所有參數的值。
* 在構造後，不能更改個別值。
* 如果指定的參數超出允許的範圍，則 `ArgumentError` 。

1. 確定初始、最小和最大比特率。
1. 確定ABR策略：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 在 `ABRControlParameters` 建構子，並將值分配給媒體播放器。

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
