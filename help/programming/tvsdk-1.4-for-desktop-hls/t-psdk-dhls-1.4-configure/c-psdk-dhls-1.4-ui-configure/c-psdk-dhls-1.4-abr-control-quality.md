---
description: HLS和DASH資料流為相同的短時連拍視訊提供不同的位元速率編碼（設定檔）。 TVSDK可以根據可用頻寬來選取每個高載的品質等級。
title: 視訊品質的最適化位元速率(ABR)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# 視訊品質的最適化位元速率(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH資料流為相同的短時連拍視訊提供不同的位元速率編碼（設定檔）。 TVSDK可以根據可用頻寬來選取每個高載的品質等級。

TVSDK會持續監控位元速率，確保內容以目前網路連線的最佳位元速率播放。

您可以設定最適化位元速率(ABR)切換原則，以及多位元速率(MBR)資料流的初始、最小和最大位元速率。 TVSDK會自動切換為位元速率，以在指定的設定中提供最佳播放體驗。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位元速率 </td> 
   <td colname="col2"> <p>第一個區段的所需播放位元速率（每秒位元數）。 開始播放時，第一個區段會使用最接近的輪廓，等於或大於初始位元速率。 </p> <p> 如果已定義最低位元速率，且初始位元速率低於最低位元速率，TVSDK會選取最低位元速率高於最低位元速率的設定檔。 如果初始速率高於最大速率，TVSDK會選取低於最大速率的最高速率。 </p> <p>如果初始位元速率為零或未定義，則初始位元速率由ABR原則決定。 </p> <p> <span class="apiname"> ABRIinitialBitRate </span> 傳回代表每秒位元組設定檔的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小位元速率 </td> 
   <td colname="col2"> <p>ABR可切換的最低允許位元速率。 ABR切換會忽略位元速率低於此位元速率的設定檔。 </p> <p> <span class="apiname"> Abriminbitrate </span> 傳回代表每秒位元設定檔的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大位元速率 </td> 
   <td colname="col2"> <p>ABR可切換的最高允許位元速率。 ABR切換會忽略位元速率高於此位元速率的設定檔。 </p> <p> <span class="apiname"> ABRMaxBitRate </span> 傳回代表每秒位元設定檔的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切換原則 </td> 
   <td colname="col2"> 儘可能讓播放逐漸切換到最高位元速率設定檔。 您可以設定ABR切換原則，以決定TVSDK在設定檔之間切換的速度。 預設值為 <span class="codeph"> MODERATE_POLICY </span>. <p>當TVSDK決定切換至較高的位元速率時，播放器會根據目前的ABR原則，選取要切換至的理想位元速率設定檔： 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> 保守原則 </span>：當頻寬比目前的位元速率高50%時，切換至具有更高位元速率的設定檔。 </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>：當頻寬比目前的位元速率高20%時，切換到下一個較高的位元速率設定檔。 </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> 積極原則 </span>：當頻寬高於目前的位元速率時，立即切換至最高位元速率設定檔。 </li> 
     </ul> </p> <p>如果初始位元速率為零或未指定，但已指定原則，則播放會從最低位元速率設定檔開始（若為保守設定）、最接近中度可用設定檔位元速率中值的設定檔，以及最高位元速率設定檔開始（若為主動設定）。 </p> <p>如果指定最小和最大位元速率，則原則會在限制中運作。 </p> <p> <span class="codeph"> ABRPolicy </span> 傳回目前設定，從 <span class="codeph"> Abrcontrolparameters </span> 列舉： CONSERVATIVE_POLICY、MODERATE_POLICY或AGGRESSIVE_POLICY。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請牢記以下資訊：

* TVSDK容錯移轉機制可能會覆寫您的設定，因為TVSDK偏好持續播放體驗，而非嚴格遵守控制引數。
* 當位元速率變更時，TVSDK會傳送 `ProfileEvent.PROFILE_CHANGED`.
* 您可以隨時變更ABR設定，播放器會切換為使用最符合最新設定的設定檔。

例如，如果資料流有下列設定檔：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果您指定300000至2000000的範圍，TVSDK只會考慮設定檔1、2和3。 這可讓應用程式根據各種網路狀況進行調整，例如從Wi-Fi切換至3G或各種裝置，例如手機、平板電腦或桌上型電腦。

若要設定ABR控制引數，請執行下列任一項作業：

* 使用 `ABRControlParameterBuilder` 協助程式類別，可設定引數的任何子集(運算於 `ABRControlParameter` 幕後)

* 在上設定引數 `ABRControlParameter` 類別。

## 使用ABRControlParametersBuilder設定最適化位元速率 {#section_3DDE397A7CE445E1832EBAA46CE5C069}

使用 `ABRControlParametersBuilder` 協助程式類別是設定ABR引數最簡單、最有效率的方式。

* 此 `ABRControlParametersBuilder` 建構函式會將所有ABR引數設定為基礎上的預設值 `ABRControlParameters` 物件。

* 只要維持對單個ABR引數的參照，您就可以在執行期間重設該引數 `ABRControlParametersBuilder` 執行個體。

此類別也包含 `toABRControlParameters()` 協助程式方法。 使用此方法取得 `ABRControlParameters` 並將其設定在 `mediaPlayer.ABRControlParameters` 屬性。 這會讓您的設定在播放器中生效。

1. 例項化 `ABRControlParametersBuilder` 協助程式類別，並在媒體播放器上設定引數。

   >[!NOTE]
   >
   >例如，下列範例將所有引數初始化為預設值，然後僅將原則設定為保守，並將最大位元速率限製為1000000：
   >
   >```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```
   >

1. 在執行階段修改個別的ABR引數。

   若要修改個別引數，同時保留其餘引數不變：

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   若要保留先前設定，您必須維持對相同設定的參照 `ABRControlParametersBuilder` 您在步驟1建立的例項。

## 使用ABRControlParameters設定最適化位元速率 {#section_02161FD0A73F40ED9CAE17F9AF850483}

您只能設定ABR控制值 `ABRControlParameters`，但您隨時可以建構新的架構。

在ABR引數存在之前，支援設定ABR引數的功能 `ABRControlParametersBuilder` 類別，但此功能在建構時設定ABR引數仍然有效。 不過，若要在建構後變更個別引數，您應使用 `ABRControlParametersBuilder` 類別。

下列條件適用於 `ABRControlParameters`：

* 您必須在建構時提供所有引數的值。
* 您無法在建構時間之後變更個別值。
* 如果您指定的引數超出允許的範圍，則 `ArgumentError` 擲回。

1. 決定初始、最小和最大位元速率。
1. 決定ABR原則：

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. 設定ABR引數值 `ABRControlParameters` 建構函式並將它們指派給媒體播放器。

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```
