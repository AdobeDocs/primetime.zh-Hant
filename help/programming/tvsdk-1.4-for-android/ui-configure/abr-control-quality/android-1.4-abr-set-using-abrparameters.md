---
description: 您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。
seo-description: 您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。
seo-title: 使用ABRControlParameters配置自適應比特率
title: 使用ABRControlParameters配置自適應比特率
uuid: c877c5cc-ad72-46dc-afc4-d41ee097a9a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 使用ABRControlParameters配置自適應比特率{#configure-adaptive-bit-rates-using-abrcontrolparameters}

您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。

下列條件適用於 `ABRControlParameters`:

* 必須在構建時提供所有參數的值。
* 在建構時間後，您無法變更個別值。
* 如果您指定的參數超出允許的範圍，則會拋出 `ArgumentError` 參數。

1. 決定初始、最小和最大位速率。
1. 確定ABR策略：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 在建構函式中設定ABR參 `ABRControlParameters` 數值，並將其指派給Media Player。

   ```java
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```

