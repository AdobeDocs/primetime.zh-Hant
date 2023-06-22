---
description: 如果您使用預設設定，則您無需執行任何其他操作即可啟用或設定帳單。 如果您從「Adobe啟用」代表取得不同的設定引數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類別設定這些引數。
title: 設定計費量度
exl-id: b49b64eb-682b-420f-9681-6e77cdb02c23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 設定計費量度 {#configure-billing-metrics}

如果您使用預設設定，則您無需執行任何其他操作即可啟用或設定帳單。 如果您從「Adobe啟用」代表取得不同的設定引數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類別設定這些引數。

>[!TIP]
>
>大部分客戶應使用預設設定。

>[!IMPORTANT]
>
>您設定的設定會在媒體播放器的一生中維持有效。 初始化媒體播放器後，便無法變更設定。

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
