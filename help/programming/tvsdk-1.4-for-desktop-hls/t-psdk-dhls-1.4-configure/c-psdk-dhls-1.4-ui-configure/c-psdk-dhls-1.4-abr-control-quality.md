---
description: HLS和DASH串流針對相同的視訊短脈衝串提供不同的位元速率編碼（描述檔）。 TVSDK可根據可用頻寬來選取每個突發串的品質等級。
seo-description: HLS和DASH串流針對相同的視訊短脈衝串提供不同的位元速率編碼（描述檔）。 TVSDK可根據可用頻寬來選取每個突發串的品質等級。
seo-title: 視訊品質的可調式位元速率(ABR)
title: 視訊品質的可調式位元速率(ABR)
uuid: e3d5ef90-067d-48e0-a025-081de931d842
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '1011'
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
   <td colname="col2"> <p>第一段的所需播放位速率（以位／秒為單位）。 當播放開始時，第一個區段會使用最接近的描述檔，該描述檔等於或大於初始位元速率。 </p> <p> 如果定義了最小位元速率，且初始位元速率低於最小速率，則TVSDK會選擇位元速率低於最小速率的描述檔。 如果初始速率高於最大速率，TVSDK會選擇低於最大速率的最高速率。 </p> <p>如果初始比特率為零或未定義，則初始比特率由ABR策略確定。 </p> <p> <span class="apiname"> ABRInitialBitRate傳 </span> 回一個整數值，代表每秒位元組描述檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最低位元速率 </td> 
   <td colname="col2"> <p>ABR可切換至的最低允許位速率。 ABR切換會忽略位速率低於此位速率的描述檔。 </p> <p> <span class="apiname"> ABRMinBitRate傳 </span> 回代表每秒位元描述檔的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大位元速率 </td> 
   <td colname="col2"> <p>ABR可切換的最高允許位速率。 ABR切換會忽略位速率高於此位速率的描述檔。 </p> <p> <span class="apiname"> ABRMaxBitRate傳 </span> 回一個整數值，代表每秒位元描述檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR交換策略 </td> 
   <td colname="col2"> 如果可能，播放會逐漸切換至最高位元速率的設定檔。 您可以設定ABR切換的原則，此原則會決定TVSDK在設定檔之間切換的速度。 預設值為<span class="codeph"> MODERATE_POLICY </span>。 <p>當TVSDK決定切換至較高的位元速率時，播放器會根據目前的ABR原則，選擇理想的位元速率描述檔以切換至： 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVAL_POLICY  </span>:當頻寬比當前位速率高50%時，切換到具有下一個較高位速率的配置檔案。 </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY  </span>:當頻寬比當前位速率高20%時，切換到下一個較高的位速率配置檔案。 </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> ACCORPICE_POLICY  </span>:當頻寬高於當前位速率時，立即切換到最高位速率配置檔案。 </li> 
     </ul> </p> <p>如果初始比特率為零或未指定，但指定了策略，則回放將從保守性的最低比特率配置檔案開始，中度可用配置檔案的中位數比特率最接近的配置檔案，以及侵略性的最高比特率配置檔案開始。 </p> <p>如果指定了最小和最大比特率，則策略在這些速率的約束下工作。 </p> <p> <span class="codeph"> ABRPolicy從 </span> ABRControlParameters枚舉返回當 <span class="codeph"> 前 </span> 設定：CONSERVACTIVE_POLICY、MODERATE_POLICY或ACCORPISIVE_POLICY。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住下列資訊：

* TVSDK容錯機制可能會覆寫您的設定，因為TVSDK偏好持續播放體驗，而非嚴格遵循您的控制參數。
* 當位元速率變更時，TVSDK會派單`ProfileEvent.PROFILE_CHANGED`。
* 您可以隨時變更ABR設定，而播放器會切換使用最符合最新設定的設定檔。

例如，如果串流具有下列描述檔：

* 1:300000
* 2:700000
* 3:150000
* 4:240000
* 5:400000

如果您指定300000到2000000的範圍，TVSDK只會考慮設定檔1、2和3。 這可讓應用程式因應各種網路狀況進行調整，例如從wi-fi切換至3G或切換至手機、平板電腦或桌上型電腦等各種裝置。

要設定ABR控制參數，請執行下列操作之一：

* 使用`ABRControlParameterBuilder`幫助類設定參數的任何子集（在後台操作`ABRControlParameter`）

* 在`ABRControlParameter`類中設定參數。

## 使用ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}設定自適應位元速率

使用`ABRControlParametersBuilder`幫助類是設定ABR參數最簡單、最有效的方法。

* `ABRControlParametersBuilder`建構子將所有ABR參數設定為基礎`ABRControlParameters`對象上的預設值。

* 只要您對相同`ABRControlParametersBuilder`實例的引用保持不變，就可以在運行時重置單個ABR參數。

此類還包括`toABRControlParameters()`幫助方法。 使用此方法可以獲取`ABRControlParameters`的實例，並在`mediaPlayer.ABRControlParameters`屬性上進行設定。 這會使您的設定在播放器中生效。

1. 實例化`ABRControlParametersBuilder`幫助程式類，並在Media Player上設定參數。

   >[!NOTE]
   >
   >例如，以下示例將所有參數初始化為預設值，然後僅將策略設定為保守，並將最大比特率限制為1000000:
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

   要修改單個參數，同時保留其餘參數原樣：

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   若要保留先前的設定，您必須保留對您在步驟1中建立之相同`ABRControlParametersBuilder`例項的參考。

## 使用ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}配置自適應位速率

您只能以`ABRControlParameters`設定ABR控制值，但可隨時建立新值。

在`ABRControlParametersBuilder`類別存在之前，支援此設定ABR參數的能力，但此能力對於在構建時設定ABR參數仍然有效。 但是，要在構建後更改單個參數，應使用`ABRControlParametersBuilder`類。

以下條件適用於`ABRControlParameters`:

* 必須在構建時提供所有參數的值。
* 在建構時間後，您無法變更個別值。
* 如果您指定的參數超出允許的範圍，則會拋出`ArgumentError`。

1. 決定初始、最小和最大位速率。
1. 確定ABR策略：

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. 在`ABRControlParameters`建構函式中設定ABR參數值，並將其指派給Media Player。

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```

