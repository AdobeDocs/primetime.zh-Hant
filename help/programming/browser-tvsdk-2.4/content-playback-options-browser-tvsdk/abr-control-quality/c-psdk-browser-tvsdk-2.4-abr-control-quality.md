---
description: HLS和DASH資料流為相同的短時連拍視訊提供不同的位元速率編碼（設定檔）。 瀏覽器TVSDK可以根據可用頻寬選取每個高載的品質等級。
title: 視訊品質的最適化位元速率(ABR)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# 概觀 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH資料流為相同的短時連拍視訊提供不同的位元速率編碼（設定檔）。 瀏覽器TVSDK可以根據可用頻寬選取每個高載的品質等級。

瀏覽器TVSDK會持續監控位元速率，確保內容以目前網路連線的最佳位元速率播放。

您可以設定最適化位元速率(ABR)切換原則，以及多位元速率(MBR)資料流的初始、最小和最大位元速率。 瀏覽器TVSDK會自動切換為位元速率，以在指定設定中提供最佳播放體驗。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位元速率 </td> 
   <td colname="col2">第一個區段的所需播放位元速率（每秒位元數）。 開始播放時，第一個區段會使用最接近的輪廓，等於或大於初始位元速率。 <p> 如果已定義最低位元速率，且初始位元速率低於最低位元速率，瀏覽器TVSDK會選取最低位元速率高於最低位元速率的設定檔。 如果初始速率高於最大速率，瀏覽器TVSDK會選取低於最大速率的最高速率。 </p> <p>如果初始位元速率為零或未定義，則初始位元速率由ABR原則決定。 </p> <p><span class="codeph"> initialBitrate</span> 傳回代表每秒位元組設定檔的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小位元速率 </td> 
   <td colname="col2">ABR可切換的最低允許位元速率。 ABR切換會忽略位元速率低於此位元速率的設定檔。 <p><span class="codeph"> minBitRate</span> 傳回代表每秒位元設定檔的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大位元速率 </td> 
   <td colname="col2">ABR可切換的最高允許位元速率。 ABR切換會忽略位元速率高於此位元速率的設定檔。 <p><span class="codeph"> maxBitRate</span> 傳回代表每秒位元設定檔的整數值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請牢記以下資訊：

* 當位元速率變更時，瀏覽器TVSDK會傳送 `AdobePSDK.ProfileEvent` 將型別設為 `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* 您可以隨時變更ABR設定，播放器會切換為使用最符合最新設定的設定檔。

例如，如果資料流有下列設定檔：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果您指定300000至2000000的範圍，瀏覽器TVSDK只會考慮設定檔1、2和3。 這可讓應用程式根據各種網路狀況進行調整，例如從Wi-Fi切換至3G或各種裝置，例如手機、平板電腦或桌上型電腦。

若要設定ABR控制引數，請執行下列動作：

* 在上設定引數 `ABRControlParameters` 類別。
