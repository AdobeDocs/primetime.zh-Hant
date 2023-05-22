---
description: HLS和DASH流為同一短視頻突發提供不同的比特率編碼（簡檔）。 TVSDK可以根據可用頻寬為每個突發選擇質量級別。
title: 用於視頻質量的自適應比特率(ABR)
exl-id: 97862cf7-7315-4ca6-a2b4-f9b98047edd9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 用於視頻質量的自適應比特率(ABR) {#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH流為同一短視頻突發提供不同的比特率編碼（簡檔）。 TVSDK可以根據可用頻寬為每個突發選擇質量級別。

TVSDK持續監視比特率以確保內容以當前網路連接的最佳比特率播放。

可以為多比特率(MBR)流設定自適應比特率(ABR)切換策略以及初始、最小和最大比特率。 TVSDK自動切換到在指定配置中提供最佳回放體驗的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段的所需重放比特率（以位/秒為單位）。 當播放開始時，最接近的輪廓（等於或大於初始比特率）用於第一段。 </p> <p> 如果定義了最小比特率並且初始比特率低於最小速率，則TVSDK選擇具有高於最小比特率的最低比特率的配置檔案。 如果初始速率高於最大速率，則TVSDK選擇低於最大速率的最高速率。 </p> <p>如果初始比特率為零或未定義，則初始比特率由ABR策略確定。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可切換到的最低允許比特率。 ABR切換忽略比此比特率更低的比特率的簡檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可切換到的最高允許比特率。 ABR切換忽略比此比特率更高的比特率的簡檔。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請牢記以下資訊：

* TVSDK不從比特率交換中調度事件。
* 您可以隨時更改ABR設定，播放器會切換使用與最近設定最接近的配置式。

例如，如果流具有以下配置檔案：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定範圍為300000到2000000，則TVSDK僅考慮配置檔案1、2和3。 這允許應用程式根據各種網路條件進行調整，例如從WiFi切換到3G或者到各種設備，如電話、平板電腦或台式電腦。

## 配置自適應比特率 {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

要配置TVSDK自適應比特率參數：

1. 配置實例 `PTABRControlParameters` 設定初始、最小和最大比特率設定。

   預設值顯示在以下代碼段中，但您的應用程式可以為這些參數中的每個參數設定任何整數值。

   >[!IMPORTANT]
   >
   >以位/秒(bps)指定位速率設定。

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. 更新 `PTMediaPlayer` 已配置實例 `PTABRControlParameters` 實例。

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

請記住以下內容：

* 應用程式必須設定 `abrControlParameters` 屬性 `PTMediaPlayer` 配置前 `PTMediaPlayerItem` 要生效的初始和最小比特率設定的實例。

   在開始內容播放後，設定新實例只影響最大比特率設定。

* 要在回放期間更新最大比特率設定，請新建 `PTABRControlParameters` 實例並將其設定在播放器實例上。
* 您只能在iOS8.0及更高版本上更新播放期間的最大比特率設定。 對於早期版本， `maxBitrate` 使用在開始內容播放之前設定的值。
