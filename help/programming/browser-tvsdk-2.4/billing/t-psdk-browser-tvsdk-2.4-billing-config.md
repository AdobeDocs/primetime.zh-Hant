---
description: 如果您使用預設設定，您就不需要執行其他動作來啟用或設定帳單。 如果您從Adobe啟用代表取得不同的設定參數，請在初始化媒體播放器之前，使用BillingMetricsConfiguration類別來設定這些參數。
title: 設定帳單量度
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 設定帳單量度{#configure-billing-metrics}

如果您使用預設設定，您就不需要執行其他動作來啟用或設定帳單。 如果您從Adobe啟用代表取得不同的設定參數，請在初始化媒體播放器之前，使用BillingMetricsConfiguration類別來設定這些參數。

大部分客戶應使用預設設定。

>[!IMPORTANT]
>
>您設定的組態在媒體播放器的使用期間仍有效。 初始化媒體播放器後，便無法變更設定。

若要設定帳單量度：

* 輸入以下代碼範例。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   其中`_player`是`AdobePSDK.MediaPlayer`的例項，而`_resource`是`AdobePSDK.MediaResource`的例項。

