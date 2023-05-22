---
description: 服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 TVSDK提供有關播放、緩衝和設備的詳細統計資訊。
title: 服務質量統計
exl-id: 7684605f-e049-47bf-8073-155d1ff000e0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 服務質量統計{#quality-of-service-statistics}

服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 TVSDK提供有關播放、緩衝和設備的詳細統計資訊。

## 讀取QOS回放、緩衝和設備統計資訊 {#section_9996406E2D814FA382B77E3041CB02BC}

可以從 `PTQOSProvider` 類。

的 `PTQOSProvider` 類提供各種統計資訊，包括有關緩衝、比特率、幀速率、時間資料等的資訊。

它還提供有關設備的資訊，如型號、作業系統和製造商的設備ID。

>[!TIP]
>
>不能更改回放緩衝區大小，但可以監視緩衝區大小的狀態以進行調試或分析。 `PTPlaybackInformation` 包括這些屬性 `playbackBufferFull` 和 `playbackLikelyToKeepUp`。

1. 實例化媒體播放器。
1. 建立 `PTQOSProvider` 對象，並將其附加到媒體播放器。

   的 `PTQOSProvider` 建構子採用播放器上下文以便能夠檢索設備特定的資訊。

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. （可選）閱讀回放統計資訊。

   讀取回放統計資訊的一個解決方案是具有計時器，例如 `NSTimer`，它定期從 `PTQOSProvider`。 例如：

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

1. （可選）讀取設備特定資訊。

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```
