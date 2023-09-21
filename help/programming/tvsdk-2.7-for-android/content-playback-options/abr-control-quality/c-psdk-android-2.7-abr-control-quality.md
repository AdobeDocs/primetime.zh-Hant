---
description: HLS和DASH資料流為相同的短時連拍視訊提供不同的位元速率編碼（設定檔）。 TVSDK可以根據目前的緩衝層級和可用頻寬，選取每個高載的品質層級。
title: 視訊品質的最適化位元速率(ABR)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---

# 概觀 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH資料流為相同的短時連拍視訊提供不同的位元速率編碼（設定檔）。 TVSDK可以根據目前的緩衝層級和可用頻寬，選取每個高載的品質層級。

TVSDK會持續監控位元速率，確保內容以目前網路連線的最佳位元速率播放。 您可以設定最適化位元速率(ABR)切換原則，以及多位元速率(MBR)資料流的初始、最小和最大位元速率。 TVSDK會自動切換為位元速率，以在指定的設定中提供最佳播放體驗。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位元速率 </td> 
   <td colname="col2"> <p>第一個區段的所需播放位元速率（每秒位元數）。 </p> <p>開始播放時，第一個區段會使用最接近的輪廓，等於或大於初始位元速率。 如果已定義最低位元速率，且初始位元速率低於最低位元速率，TVSDK會選取最低位元速率高於最低位元速率的設定檔。 如果初始速率高於最大速率，TVSDK會選取低於最大速率的最高速率。 如果初始位元速率為零或未定義，則初始位元速率由ABR原則決定。 </p> <p><span class="codeph"> getABRIinitialBitRate</span> 傳回代表每秒位元組設定檔的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小位元速率 </td> 
   <td colname="col2"> <p>ABR可切換的最低允許位元速率。 </p> <p>ABR切換會忽略位元速率低於此位元速率的設定檔。 <span class="codeph"> getABRMinBitrate</span> 傳回代表每秒位元設定檔的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大位元速率 </td> 
   <td colname="col2"> <p>ABR可切換的最高允許位元速率。 </p> <p>ABR切換會忽略位元速率高於此位元速率的設定檔。 <span class="codeph"> getABRMaxBitRate</span> 傳回代表每秒位元設定檔的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切換原則 </td> 
   <td colname="col2"> <p>儘可能讓播放逐漸切換到最高位元速率設定檔。 您可以設定ABR切換原則，以決定TVSDK在設定檔之間切換的速度。 預設值為 <span class="codeph"> ABR_MODERATE</span>. </p> <p>當TVSDK決定切換至較高的位元速率時，播放器會根據目前的ABR原則，選取要切換至的理想位元速率設定檔： 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>：當頻寬比目前的位元速率高50%時，切換至具有更高位元速率的設定檔。 </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>：當頻寬比目前的位元速率高20%時，切換到下一個較高的位元速率設定檔。 </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>：當頻寬高於目前的位元速率時，立即切換至最高位元速率設定檔。 </li> 
     </ul> </p> <p>如果初始位元速率為零，或未指定但指定原則，則播放會從保守原則的最低位元速率設定檔、最接近中度原則可用設定檔位元速率中值的設定檔，以及積極原則的最高位元速率設定檔開始。 </p> <p>如果指定最小和最大位元速率，則原則會在限制中運作。 </p> <p> <span class="codeph"> getABRPolicy</span> 傳回目前設定，從 <span class="codeph"> Abrcontrolparameters</span> 列舉： <span class="codeph"> ABR_CONSERVATIVE</span>， <span class="codeph"> ABR_MODERATE</span>，或 <span class="codeph"> ABR_AGGRESSIVE</span>. </p> <p>如需詳細資訊，請參閱ABRControlParameters API檔案。</p> </td> 
  </tr> 
 </tbody> 
</table>

請牢記以下資訊：

* TVSDK容錯移轉機制可能會覆寫您的設定，因為TVSDK偏好持續播放體驗，而非嚴格遵守控制引數。
* 當位元速率變更時，TVSDK會傳送 `onProfileChanged` 中的事件 `PlaybackEventListener`.

* 您可以隨時變更ABR設定，播放器會切換為使用最符合最新設定的設定檔。

例如，如果資料流有下列設定檔：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果您指定300000至2000000的範圍，TVSDK只會考慮設定檔1、2和3。 這可讓應用程式根據各種網路狀況進行調整，例如從Wi-Fi切換至3G或各種裝置，例如手機、平板電腦或桌上型電腦。

若要設定ABR控制引數，請在 `ABRControlParameter` 類別。
