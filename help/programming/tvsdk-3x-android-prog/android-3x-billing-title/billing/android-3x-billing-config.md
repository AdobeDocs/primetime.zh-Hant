---
description: 如果您使用預設設定，您就不需要執行其他動作來啟用或設定帳單。 如果您從Adobe啟用代表取得不同的設定參數，請在初始化媒體播放器之前，使用BillingMetricsConfiguration類別來設定這些參數。
seo-description: 如果您使用預設設定，您就不需要執行其他動作來啟用或設定帳單。 如果您從Adobe啟用代表取得不同的設定參數，請在初始化媒體播放器之前，使用BillingMetricsConfiguration類別來設定這些參數。
seo-title: 設定帳單量度
title: 設定帳單量度
uuid: 340439bf-185b-4761-a481-010908842811
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# 設定帳單量度{#configure-billing-metrics}

如果您使用預設設定，您就不需要執行其他動作來啟用或設定帳單。 如果您從Adobe啟用代表取得不同的設定參數，請在初始化媒體播放器之前，使用BillingMetricsConfiguration類別來設定這些參數。

>[!TIP]
>
>大部分客戶應使用預設設定。

>[!IMPORTANT]
>
>您設定的組態在媒體播放器的使用期間仍有效。 初始化媒體播放器後，便無法變更設定。

若要設定帳單量度：

輸入以下代碼範例。

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
