---
description: HLS和DASH資料流為相同的短時突發視訊提供不同的位元速率編碼（設定檔）。 TVSDK可以根據可用頻寬來選取每個高載的品質等級。
title: 視訊品質的最適化位元速率(ABR)
exl-id: dd6d091a-58c9-4825-8c2c-a1257ef37f22
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 視訊品質的最適化位元速率(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH資料流為相同的短時突發視訊提供不同的位元速率編碼（設定檔）。 TVSDK可以根據可用頻寬來選取每個高載的品質等級。

TVSDK會持續監控位元速率，以確保內容以目前網路連線的最佳位元速率播放。

您可以設定最適化位元速率(ABR)切換原則，以及多位元速率(MBR)資料流的初始、最小和最大位元速率。 TVSDK會自動切換至在指定設定中提供最佳播放體驗的位元速率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位元速率 </td> 
   <td colname="col2"> <p>第一個區段的所需播放位元速率（以位元/秒為單位）。 當播放開始時，第一個區段會使用最接近的設定檔（等於或大於初始位元速率）。 </p> <p> 如果已定義最低位元速率，且初始位元速率低於最低位元速率，TVSDK會選取最低位元速率高於最低位元速率的設定檔。 如果初始速率高於最大速率，TVSDK會選取低於最大速率的最高速率。 </p> <p>如果初始位元速率為零或未定義，初始位元速率會由ABR原則決定。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小位元速率 </td> 
   <td colname="col2"> <p>ABR可切換的最低位元速率。 ABR切換會忽略位元速率低於此位元速率的設定檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大位元速率 </td> 
   <td colname="col2"> <p>ABR可切換的最高允許位元速率。 ABR切換會忽略位元速率高於此位元速率的設定檔。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住下列資訊：

* TVSDK不會從位元速率切換傳送事件。
* 您可以隨時變更ABR設定，然後播放器會切換成使用最符合最新設定的設定檔。

例如，如果串流具有以下設定檔：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果您指定300000至2000000的範圍，TVSDK只會考慮設定檔1、2和3。 這可讓應用程式根據各種網路狀況進行調整，例如從WiFi切換至3G或各種裝置，例如手機、平板電腦或桌上型電腦。

## 設定最適化位元速率 {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

若要設定TVSDK最適化位元速率引數：

1. 設定執行個體 `PTABRControlParameters` 設定初始、最小和最大位元速率設定。

   預設值會顯示在下列程式碼片段中，但您的應用程式可針對每個引數設定任何整數值。

   >[!IMPORTANT]
   >
   >以每秒位元(bps)指定位元速率設定。

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. 更新您的 `PTMediaPlayer` 執行個體已設定 `PTABRControlParameters` 執行個體。

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

請記住以下事項：

* 應用程式必須設定 `abrControlParameters` 屬性： `PTMediaPlayer` 設定前 `PTMediaPlayerItem` 初始位元速率和最小位元速率設定的例項生效。

   開始播放內容後，設定新例項只會影響最大位元速率設定。

* 若要在播放期間更新最大位元速率設定，請建立新的 `PTABRControlParameters` 執行個體，並在播放器執行個體上加以設定。
* 您只能在iOS 8.0和更新版本上，在播放期間更新最大位元速率設定。 若為舊版， `maxBitrate` 使用內容播放開始前所設定的值。
