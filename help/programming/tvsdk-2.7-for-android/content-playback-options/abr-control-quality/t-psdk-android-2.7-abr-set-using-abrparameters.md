---
description: 您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。
seo-description: 您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。
seo-title: 使用ABRControlParameters配置自適應比特率
title: 使用ABRControlParameters配置自適應比特率
uuid: 7084e954-196b-492e-846f-f8b36bed13a9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '141'
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

