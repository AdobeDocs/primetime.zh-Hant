---
description: 您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。
seo-description: 您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。
seo-title: 使用ABRControlParameters配置自適應比特率
title: 使用ABRControlParameters配置自適應比特率
uuid: 99b7a463-327b-48bf-8244-e41467072b44
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 使用ABRControlParameters配置自適應比特率{#configure-adaptive-bit-rates-using-abrcontrolparameters}

您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新值。

下列條件適用於 `ABRControlParameters`:

* 必須在構建時提供所有參數的值。
* 在建構時間後，您無法變更個別值。
* 如果您指定的參數超出允許的範圍，則會拋出 `ArgumentError` 參數。

1. 確定ABR策略：

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. 在建構函式中設定ABR參 `ABRControlParameters` 數值，並將其指派給Media Player。

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```

