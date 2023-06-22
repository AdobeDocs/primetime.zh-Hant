---
description: 您只能使用ABRControlParameters設定ABR控制值，但您可以隨時建構新的控制值。
title: 使用ABRControlParameters設定最適化位元速率
exl-id: 53ca8516-b449-46c8-baa9-9d0d5800b3c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# 使用ABRControlParameters設定最適化位元速率{#configure-adaptive-bit-rates-using-abrcontrolparameters}

您只能使用ABRControlParameters設定ABR控制值，但您可以隨時建構新的控制值。

下列條件適用於 `ABRControlParameters`：

* 您必須在建構時提供所有引數的值。
* 您無法在建構時間之後變更個別值。
* 如果您指定的引數超出允許的範圍，則 `ArgumentError` 擲回。

1. 確定ABR原則：

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. 將ABR引數值設定在 `ABRControlParameters` 建構函式並將它們指派給媒體播放器。

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```
