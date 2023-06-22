---
description: 如果您使用預設設定，則您無需執行任何其他操作即可啟用或設定帳單。 如果您從「Adobe啟用」代表取得不同的設定引數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類別設定這些引數。
title: 設定計費量度
exl-id: 1eb50822-77a0-4b3a-a84c-b6082bcd1cad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 設定計費量度{#configure-billing-metrics}

如果您使用預設設定，則您無需執行任何其他操作即可啟用或設定帳單。 如果您從「Adobe啟用」代表取得不同的設定引數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類別設定這些引數。

大部分客戶應使用預設設定。

>[!IMPORTANT]
>
>您設定的設定會在媒體播放器的一生中維持有效。 初始化媒體播放器後，便無法變更設定。

若要設定計費量度：

* 輸入下列程式碼範例。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   位置 `_player` 為的例項 `AdobePSDK.MediaPlayer` 和 `_resource` 為的例項 `AdobePSDK.MediaResource`.
