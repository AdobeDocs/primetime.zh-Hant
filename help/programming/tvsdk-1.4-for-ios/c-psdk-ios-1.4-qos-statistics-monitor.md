---
description: 服務品質(QoS)提供視訊引擎執行狀況的詳細檢視。 TVSDK提供有關播放、緩衝和裝置的詳細統計資料。
title: 服務品質統計資料
exl-id: 7684605f-e049-47bf-8073-155d1ff000e0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 服務品質統計資料{#quality-of-service-statistics}

服務品質(QoS)提供視訊引擎執行狀況的詳細檢視。 TVSDK提供有關播放、緩衝和裝置的詳細統計資料。

## 讀取QOS播放、緩衝和裝置統計資料 {#section_9996406E2D814FA382B77E3041CB02BC}

您可以讀取播放、緩衝和裝置統計資料，從 `PTQOSProvider` 類別。

此 `PTQOSProvider` class提供各種統計資料，包括關於緩衝、位元速率、影格速率、時間資料等的資訊。

它也提供裝置的相關資訊，例如型號、作業系統和製造商的裝置ID。

>[!TIP]
>
>您無法變更播放緩衝區大小，但可以監控緩衝區大小的狀態，以便進行偵錯或分析。 `PTPlaybackInformation` 包括以下屬性 `playbackBufferFull` 和 `playbackLikelyToKeepUp`.

1. 例項化媒體播放器。
1. 建立 `PTQOSProvider` 物件並將其附加至媒體播放器。

   此 `PTQOSProvider` 建構函式會擷取播放器內容，以便擷取裝置特定資訊。

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. （選用）讀取播放統計資料。

   讀取播放統計資料的解決方案之一，就是使用計時器，例如 `NSTimer`，會定期從擷取新的QoS值 `PTQOSProvider`. 例如：

   ```
   - (void)printPlaybackInfoLog { 
       PTPlaybackInformation *playbackInfo = qosProvider.playbackInformation;  
       if (playbackInfo) { 
           // For example: 
           NSString *infoLog = [NSString stringWithFormat:@"observedBitrate :  
                                  %f\n",playbackInfo.observedBitrate]; 
           [consoleView logMessage:@"====%@\n\n",infoLog]; 
       } 
   }
   ```

1. （選擇性）讀取裝置特定資訊。

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```
