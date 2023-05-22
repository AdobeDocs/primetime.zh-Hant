---
description: 如果使用預設配置，則無需執行其他任何操作即可啟用或配置計費。 如果您從Adobe啟用代表處獲得了不同的配置參數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類設定這些參數。
title: 配置計費度量
exl-id: b49b64eb-682b-420f-9681-6e77cdb02c23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 配置計費度量 {#configure-billing-metrics}

如果使用預設配置，則無需執行其他任何操作即可啟用或配置計費。 如果您從Adobe啟用代表處獲得了不同的配置參數，請在初始化媒體播放器之前使用BillingMetricsConfiguration類設定這些參數。

>[!TIP]
>
>大多數客戶應使用預設配置。

>[!IMPORTANT]
>
>您設定的配置在媒體播放器的生命週期中仍然有效。 初始化媒體播放器後，無法更改配置。

要配置計費度量，請執行以下操作：

1. 輸入以下代碼樣例。

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
