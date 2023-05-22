---
description: 您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新的控制值。
title: 使用ABRControlParameters配置自適應比特率
exl-id: 53ca8516-b449-46c8-baa9-9d0d5800b3c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# 使用ABRControlParameters配置自適應比特率{#configure-adaptive-bit-rates-using-abrcontrolparameters}

您只能使用ABRControlParameters設定ABR控制值，但可以隨時構造新的控制值。

以下條件適用於 `ABRControlParameters`:

* 必須在構造時為所有參數提供值。
* 在構建時間後不能更改單個值。
* 如果指定的參數超出允許的範圍，則 `ArgumentError` 。

1. 確定ABR策略：

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. 在 `ABRControlParameters` 建構子，並將其分配給媒體播放器。

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```
