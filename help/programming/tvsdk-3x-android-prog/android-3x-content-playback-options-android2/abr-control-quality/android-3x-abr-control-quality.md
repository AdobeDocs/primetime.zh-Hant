---
description: HLS和DASH流為同一短視頻突發提供不同的比特率編碼（簡檔）。 TVSDK可以根據當前緩衝級別和可用頻寬為每個突發選擇質量級別。
title: 用於視頻質量的自適應比特率(ABR)
exl-id: ed062ef9-138d-446a-a454-3cb19c3bb388
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# 概述 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH流為同一短視頻突發提供不同的比特率編碼（簡檔）。 TVSDK可以根據當前緩衝級別和可用頻寬為每個突發選擇質量級別。

TVSDK持續監視比特率以確保內容以當前網路連接的最佳比特率播放。 可以設定多比特率(MBR)流的自適應比特率(ABR)切換策略和初始、最小和最大比特率。 TVSDK自動切換到在指定配置中提供最佳回放體驗的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段的所需重放比特率（以位/秒為單位）。 </p> <p>當播放開始時，最接近的輪廓（等於或大於初始比特率）用於第一段。 如果定義了最小比特率並且初始比特率低於最小速率，則TVSDK選擇具有高於最小比特率的最低比特率的配置檔案。 如果初始速率高於最大速率，則TVSDK選擇低於最大速率的最高速率。 如果初始比特率為零或未定義，則初始比特率由ABR策略確定。 </p> <p><span class="codeph"> getABRInitialBitRate</span> 返回表示每秒位元組配置檔案的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可切換到的最低允許比特率。 </p> <p>ABR切換忽略比此比特率更低的比特率的簡檔。 <span class="codeph"> getABRMinBitRate</span> 返回表示每秒位配置檔案的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可切換到的最高允許比特率。 </p> <p>ABR切換忽略比此比特率更高的比特率的簡檔。 <span class="codeph"> getABRMaxBitRate</span> 返回表示每秒位配置檔案的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切換策略 </td> 
   <td colname="col2"> <p>如果可能，回放將逐漸切換到最高比特率配置檔案。 您可以設定ABR切換策略，該策略確定TVSDK在配置檔案之間切換的速度。 預設值為 <span class="codeph"> ABR(_M)</span>。 </p> <p>當TVSDK決定切換到較高的比特率時，播放器根據當前的ABR策略選擇理想的比特率配置檔案以切換到： 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVAL</span>:當頻寬比當前比特率高50%時，切換到具有下一個更高比特率的配置式。 </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR(_M)</span>:當頻寬比當前比特率高20%時，切換到下一個更高的比特率配置檔案。 </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_ACCIVE</span>:當頻寬高於當前比特率時，立即切換到最高比特率配置檔案。 </li> 
     </ul> </p> <p>如果初始比特率為零，或未指定但指定了策略，則回放從保守策略的最低比特率配置檔案、最接近中等策略的可用配置檔案的中位數比特率的配置檔案以及激進策略的最高比特率配置檔案開始。 </p> <p>如果指定了這些速率，則策略在最小和最大比特率的約束下工作。 </p> <p> <span class="codeph"> getABRPolicy</span> 從 <span class="codeph"> ABRControlParameters</span> 枚舉： <span class="codeph"> ABR_CONSERVAL</span>。 <span class="codeph"> ABR(_M)</span>或 <span class="codeph"> ABR_ACCIVE</span>。 </p> <p>有關詳細資訊，請參閱ABR Control Parameters API文檔。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請牢記以下資訊：

* TVSDK故障轉移機制可能會覆蓋您的設定，因為TVSDK更青睞連續的回放體驗，而不是嚴格遵循您的控制參數。
* 當比特率更改時，TVSDK派單 `onProfileChanged` 事件 `PlaybackEventListener`。

* 您可以隨時更改ABR設定，播放器會切換使用與最近設定最接近的配置式。

例如，如果流具有以下配置檔案：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定範圍為300000到2000000，則TVSDK僅考慮配置檔案1、2和3。 這允許應用程式根據各種網路條件進行調整，例如從wi-fi切換到3G或切換到各種設備，如電話、平板或台式電腦。

要設定ABR控制參數，請在 `ABRControlParameter` 類。
