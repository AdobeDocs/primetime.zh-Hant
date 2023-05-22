---
description: HLS和DASH流為同一短視頻突發提供不同的比特率編碼（簡檔）。 TVSDK可以根據可用頻寬為每個突發選擇質量級別。
title: 用於視頻質量的自適應比特率(ABR)
exl-id: 2fd24360-4159-4330-a479-02310c6aa525
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# 用於視頻質量的自適應比特率(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH流為同一短視頻突發提供不同的比特率編碼（簡檔）。 TVSDK可以根據可用頻寬為每個突發選擇質量級別。

TVSDK持續監視比特率以確保內容以當前網路連接的最佳比特率播放。

可以為多比特率(MBR)流設定自適應比特率(ABR)切換策略以及初始、最小和最大比特率。 TVSDK自動切換到在指定配置中提供最佳回放體驗的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段的所需重放比特率（以位/秒為單位）。 當播放開始時，最接近的輪廓（等於或大於初始比特率）用於第一段。 </p> <p> 如果定義了最小比特率並且初始比特率低於最小速率，則TVSDK選擇具有高於最小比特率的最低比特率的配置檔案。 如果初始速率高於最大速率，則TVSDK選擇低於最大速率的最高速率。 </p> <p>如果初始比特率為零或未定義，則初始比特率由ABR策略確定。 </p> <p> <span class="apiname"> ABRInitialBitRate </span> 返回表示每秒位元組配置檔案的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可切換到的最低允許比特率。 ABR切換忽略比此比特率更低的比特率的簡檔。 </p> <p> <span class="apiname"> ABRMinBitRate </span> 返回表示每秒位配置檔案的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可切換到的最高允許比特率。 ABR切換忽略比此比特率更高的比特率的簡檔。 </p> <p> <span class="apiname"> ABRMaxBitRate </span> 返回表示每秒位配置檔案的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切換策略 </td> 
   <td colname="col2"> 如果可能，回放將逐漸切換到最高比特率配置檔案。 您可以設定ABR切換策略，該策略確定TVSDK在配置檔案之間切換的速度。 預設值為 <span class="codeph"> 中等策略 </span>。 <p>當TVSDK決定切換到較高的比特率時，播放器根據當前的ABR策略選擇理想的比特率配置檔案以切換到： 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVAL_POLICY </span>:當頻寬比當前比特率高50%時，切換到具有下一個更高比特率的配置式。 </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> 中等策略 </span>:當頻寬比當前比特率高20%時，切換到下一個更高的比特率配置檔案。 </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> 攻擊性策略 </span>:當頻寬高於當前比特率時，立即切換到最高比特率配置檔案。 </li> 
     </ul> </p> <p>如果初始比特率為零或未指定，但指定了策略，則回放從保守的最低比特率配置檔案開始，中等的最接近可用配置檔案的中位比特率的配置檔案，和侵略的最高比特率配置檔案開始。 </p> <p>如果指定了這些速率，則策略在最小和最大比特率的約束下工作。 </p> <p> <span class="codeph"> ABRP策略 </span> 從 <span class="codeph"> ABRControlParameters </span> 枚舉：CONSERVATIVE_POLICY、MEDATE_POLICY或ACCIVE_POLICY。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請牢記以下資訊：

* TVSDK故障轉移機制可能會覆蓋您的設定，因為TVSDK更青睞連續的回放體驗，而不是嚴格遵循您的控制參數。
* 當比特率更改時，TVSDK派單 `ProfileEvent.PROFILE_CHANGED`。
* 您可以隨時更改ABR設定，播放器會切換使用與最近設定最接近的配置式。

例如，如果流具有以下配置檔案：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定範圍為300000到2000000，則TVSDK僅考慮配置檔案1、2和3。 這允許應用程式根據各種網路條件進行調整，例如從wi-fi切換到3G或切換到各種設備，如電話、平板或台式電腦。

要設定ABR控制參數，請執行以下操作之一：

* 使用 `ABRControlParameterBuilder` 幫助類，用於設定參數的任何子集(在 `ABRControlParameter` 幕後)

* 在 `ABRControlParameter` 類。

## 使用ABRControlParametersBuilder配置自適應比特率 {#section_3DDE397A7CE445E1832EBAA46CE5C069}

使用 `ABRControlParametersBuilder` helper類是設定ABR參數的最簡單、最有效的方法。

* 的 `ABRControlParametersBuilder` 建構子將所有ABR參數設定為基礎上的預設值 `ABRControlParameters` 的雙曲餘切值。

* 只要在運行時保留對同一參數的參照，就可以在運行期間重置單個ABR參數 `ABRControlParametersBuilder` 實例。

此類還包括 `toABRControlParameters()` helper方法。 使用此方法獲取 `ABRControlParameters` 然後把它放在 `mediaPlayer.ABRControlParameters` 屬性。 這會使您的設定在播放器中生效。

1. 實例化 `ABRControlParametersBuilder` 幫助程式類，並在媒體播放器上設定參數。

   >[!NOTE]
   >
   >例如，以下示例將所有參數初始化為預設值，然後僅將策略設定為conservaty，並將最大比特率限制為1000000:
   >
   >
   ```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```

1. 在運行時修改單個ABR參數。

   要修改單個參數，同時保留其餘參數：

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   要保留以前的設定，必須保留對該設定的引用 `ABRControlParametersBuilder` 在步驟1中建立的實例。

## 使用ABRControlParameters配置自適應比特率 {#section_02161FD0A73F40ED9CAE17F9AF850483}

您只能使用 `ABRControlParameters`，但可以隨時構造新的。

在ABR存在之前，支援設定ABR參數的這一能力 `ABRControlParametersBuilder` 但該能力對於在施工時設定ABR參數仍然有效。 但是，要在構建後更改單個參數，應使用 `ABRControlParametersBuilder` 類。

以下條件適用於 `ABRControlParameters`:

* 必須在構造時為所有參數提供值。
* 在構建時間後不能更改單個值。
* 如果指定的參數超出允許的範圍，則 `ArgumentError` 。

1. 確定初始、最小和最大比特率。
1. 確定ABR策略：

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. 在 `ABRControlParameters` 建構子，並將其分配給媒體播放器。

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```
