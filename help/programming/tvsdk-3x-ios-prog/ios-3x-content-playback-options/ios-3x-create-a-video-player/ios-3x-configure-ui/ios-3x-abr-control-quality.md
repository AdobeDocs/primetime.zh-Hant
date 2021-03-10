---
description: HLS和DASH串流針對相同的視訊短脈衝串提供不同的位元速率編碼（描述檔）。 TVSDK可根據可用頻寬來選取每個突發串的品質等級。
title: 視訊品質的可調式位元速率(ABR)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---


# 視訊品質的可調式位元速率(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH串流針對相同的視訊短脈衝串提供不同的位元速率編碼（描述檔）。 TVSDK可根據可用頻寬來選取每個突發串的品質等級。

TVSDK會持續監視位元速率，以確保內容以目前網路連線的最佳位元速率播放。

您可以為多位速率(MBR)串流設定自適應位速率(ABR)切換策略和初始、最小和最大位速率。 TVSDK會自動切換至位元速率，以在指定組態中提供最佳播放體驗。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位元速率 </td> 
   <td colname="col2"> <p>第一段的所需播放位速率（以位／秒為單位）。 當播放開始時，第一個區段會使用最接近的描述檔，該描述檔等於或大於初始位元速率。 </p> <p> 如果定義了最小位元速率，且初始位元速率低於最小速率，則TVSDK會選擇位元速率低於最小速率的描述檔。 如果初始速率高於最大速率，TVSDK會選擇低於最大速率的最高速率。 </p> <p>如果初始比特率為零或未定義，則初始比特率由ABR策略確定。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最低位元速率 </td> 
   <td colname="col2"> <p>ABR可切換至的最低允許位速率。 ABR切換會忽略位速率低於此位速率的描述檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大位元速率 </td> 
   <td colname="col2"> <p>ABR可切換的最高允許位速率。 ABR切換會忽略位速率高於此位速率的描述檔。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住下列資訊：

* TVSDK不會從位速率切換中分派事件。
* 您可以隨時變更ABR設定，而播放器會切換使用最符合最新設定的設定檔。

例如，如果串流具有下列描述檔：

* 1:300000
* 2:700000
* 3:150000
* 4:240000
* 5:400000

如果您指定300000到2000000的範圍，TVSDK只會考慮設定檔1、2和3。 這可讓應用程式因應各種網路狀況進行調整，例如從WiFi切換至3G或切換至手機、平板電腦或桌上型電腦等各種裝置。

## 配置自適應位速率{#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

若要設定TVSDK可調式位元速率參數：

1. 配置`PTABRControlParameters`實例以設定初始、最小和最大位速率設定。

   預設值會顯示在下列程式碼片段中，但您的應用程式可針對每個參數設定任何整數值。

   >[!IMPORTANT]
   >
   >以每秒位數(bps)為單位指定位速率設定。

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. 使用已配置的`PTABRControlParameters`實例更新您的`PTMediaPlayer`實例。

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

請記住：

* 應用程式必須先在`PTMediaPlayer`上設定`abrControlParameters`屬性，才能設定`PTMediaPlayerItem`例項，讓初始和最小位元速率設定生效。

   內容播放開始後，設定新例項只會影響最大位元速率設定。

* 若要在播放期間更新最大位元速率設定，請建立新的`PTABRControlParameters`例項，並在播放器例項上加以設定。
* 您只能在iOS 8.0和更新版本上，在播放期間更新最大位元速率設定。 對於舊版，會使用在內容播放開始前設定的`maxBitrate`值。