---
description: 您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。
title: 使用ABRControlParameters配置自適應比特率
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# 使用ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}配置自適應位速率

您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。

以下條件適用於`ABRControlParameters`:

* 在構建時，必須為所有參數提供值。
* 在建構後，您無法變更個別值。
* 如果您指定的參數超出允許的範圍，則會拋出`ArgumentError`。

1. 確定初始、最小和最大位速率。
1. 確定ABR策略：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 在`ABRControlParameters`建構函式中設定ABR參數值，並將值指派給Media Player。

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
