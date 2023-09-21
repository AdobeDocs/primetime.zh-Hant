---
description: 如果您使用預設設定，則您不需要執行其他操作即可啟用或設定帳單。 如果您從「Adobe啟用」代表取得不同的設定引數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類別設定這些引數。
title: 設定計費量度
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 設定計費量度 {#configure-billing-metrics}

如果您使用預設設定，則您不需要執行其他操作即可啟用或設定帳單。 如果您從「Adobe啟用」代表取得不同的設定引數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類別設定這些引數。

>[!TIP]
>
>大部分客戶應使用預設設定。

>[!IMPORTANT]
>
>您設定的設定會在媒體播放器的有效期內維持有效。 初始化媒體播放器後，便無法變更設定。

若要設定計費量度：

1. 輸入下列程式碼範例。

   ```java
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   BillingMetricsConfiguration billingConfig = new BillingMetricsConfiguration(); 
   billingConfig.setEnabled(true); 
   billingConfig.setProVODBillableDurationMinutes(60); 
   billingConfig.setStdVODBillableDurationMinutes(30); 
   billingConfig.setLiveBillableDurationMinutes(15); 
   config.setBillingMetricsConfiguration(billingConfig); 
   mediaPlayer.replaceCurrentResource(mediaResource, config);
   ```
