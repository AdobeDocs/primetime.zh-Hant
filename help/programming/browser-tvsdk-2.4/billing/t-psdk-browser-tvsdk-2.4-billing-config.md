---
description: 如果使用預設配置，則無需執行其他任何操作即可啟用或配置計費。 如果您從Adobe啟用代表處獲得了不同的配置參數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類設定這些參數。
title: 配置計費度量
exl-id: 1eb50822-77a0-4b3a-a84c-b6082bcd1cad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 配置計費度量{#configure-billing-metrics}

如果使用預設配置，則無需執行其他任何操作即可啟用或配置計費。 如果您從Adobe啟用代表處獲得了不同的配置參數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類設定這些參數。

大多數客戶應使用預設配置。

>[!IMPORTANT]
>
>您設定的配置在媒體播放器的生命週期中仍然有效。 初始化媒體播放器後，無法更改配置。

要配置計費度量，請執行以下操作：

* 輸入以下代碼樣例。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   何處 `_player` 是 `AdobePSDK.MediaPlayer` 和 `_resource` 是 `AdobePSDK.MediaResource`。
