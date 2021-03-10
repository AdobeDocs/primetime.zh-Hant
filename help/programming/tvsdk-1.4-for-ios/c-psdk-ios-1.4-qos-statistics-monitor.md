---
description: 服務品質(QoS)提供視訊引擎執行情形的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。
title: 服務質量統計
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# 服務質量統計資料{#quality-of-service-statistics}

服務品質(QoS)提供視訊引擎執行情形的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。

## 讀取QOS回放、緩衝和設備統計資訊{#section_9996406E2D814FA382B77E3041CB02BC}

您可以從`PTQOSProvider`類別讀取播放、緩衝和裝置統計資料。

`PTQOSProvider`類別提供各種統計資料，包括緩衝、位元速率、影格速率、時間資料等資訊。

它也提供有關裝置的資訊，例如機型、作業系統和製造商的裝置ID。

>[!TIP]
>
>您無法變更播放緩衝區大小，但可以監視緩衝區大小的狀態，以便進行調試或分析。 `PTPlaybackInformation` 包含和等 `playbackBufferFull` 屬性 `playbackLikelyToKeepUp`。

1. 實例化媒體播放器。
1. 建立`PTQOSProvider`物件，並將它附加至媒體播放器。

   `PTQOSProvider`建構函式會擷取播放器內容，以便擷取裝置特定資訊。

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. （可選）閱讀播放統計資料。

   讀取播放統計資訊的一個解決方案是具有一個計時器，如從`PTQOSProvider`週期性地讀取新QoS值的`NSTimer`。 例如：

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

1. （可選）閱讀裝置特定資訊。

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```

