---
description: 服務品質(QoS)可提供視訊引擎執行狀況的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。
title: 服務品質統計資料
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 服務品質統計資料{#quality-of-service-statistics}

服務品質(QoS)可提供視訊引擎執行狀況的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。

## 讀取QOS播放、緩衝和裝置統計資料 {#section_9996406E2D814FA382B77E3041CB02BC}

您可以讀取播放、緩衝和裝置統計資料，從 `PTQOSProvider` 類別。

此 `PTQOSProvider` class提供各種統計資料，包括有關緩衝、位元速率、影格速率、時間資料的資訊，等等。

它也會提供裝置的相關資訊，例如型號、作業系統和製造商的裝置ID。

>[!TIP]
>
>您無法變更播放緩衝區大小，但可以監視緩衝區大小的狀態以進行偵錯或分析。 `PTPlaybackInformation` 包括以下屬性 `playbackBufferFull` 和 `playbackLikelyToKeepUp`.

1. 例項化媒體播放器。
1. 建立 `PTQOSProvider` 物件並將其附加至媒體播放器。

   此 `PTQOSProvider` 建構函式會擷取播放器內容，以便擷取裝置特定資訊。

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. （選用）讀取播放統計資料。

   讀取播放統計資料的解決方案之一是擁有計時器，例如 `NSTimer`，會定期從擷取新的QoS值 `PTQOSProvider`. 例如：

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
