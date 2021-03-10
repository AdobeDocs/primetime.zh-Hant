---
description: HLS和DASH串流針對相同的視訊短脈衝串提供不同的位元速率編碼（描述檔）。 TVSDK可根據目前的緩衝層級和可用頻寬，來選取每個突發串的品質層級。
title: 視訊品質的可調式位元速率(ABR)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---


# 概述{#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH串流針對相同的視訊短脈衝串提供不同的位元速率編碼（描述檔）。 TVSDK可根據目前的緩衝層級和可用頻寬，來選取每個突發串的品質層級。

TVSDK會持續監視位元速率，以確保內容以目前網路連線的最佳位元速率播放。 您可以為多位元速率(MBR)串流設定自適應位元速率(ABR)切換原則以及初始、最小和最大位元速率。 TVSDK會自動切換至位元速率，以在指定組態中提供最佳播放體驗。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位元速率 </td> 
   <td colname="col2"> <p>第一段的所需播放位速率（以位／秒為單位）。 </p> <p>當播放開始時，第一個區段會使用最接近的描述檔，該描述檔等於或大於初始位元速率。 如果定義了最小位元速率，且初始位元速率低於最小速率，則TVSDK會選擇位元速率低於最小速率的描述檔。 如果初始速率高於最大速率，TVSDK會選擇低於最大速率的最高速率。 如果初始比特率為零或未定義，則初始比特率由ABR策略確定。 </p> <p><span class="codeph"> </span> getABRInitialBitRate會傳回整數值，代表每秒位元組描述檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最低位元速率 </td> 
   <td colname="col2"> <p>ABR可切換至的最低允許位速率。 </p> <p>ABR切換會忽略位速率低於此位速率的描述檔。 <span class="codeph"> </span> getABRMinBitRate會傳回一個整數值，代表每秒位元描述檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大位元速率 </td> 
   <td colname="col2"> <p>ABR可切換的最高允許位速率。 </p> <p>ABR切換會忽略位速率高於此位速率的描述檔。 <span class="codeph"> </span> getABRMaxBitRate會傳回一個整數值，代表每秒位元描述檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR交換策略 </td> 
   <td colname="col2"> <p>如果可能，播放會逐漸切換至最高位元速率的設定檔。 您可以設定ABR切換的原則，此原則會決定TVSDK在設定檔之間切換的速度。 預設值為<span class="codeph"> ABR_MODERATE</span>。 </p> <p>當TVSDK決定切換至較高的位元速率時，播放器會根據目前的ABR原則，選擇理想的位元速率描述檔以切換至： 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVACY</span>:當頻寬比當前位速率高50%時，切換到具有下一個較高位速率的配置檔案。 </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>:當頻寬比當前位速率高20%時，切換到下一個較高的位速率配置檔案。 </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_ACCORPISE</span>:當頻寬高於當前位速率時，立即切換到最高位速率配置檔案。 </li> 
     </ul> </p> <p>如果初始位速率為零，或未指定但指定了策略，則回放將從保守策略的最低位速率配置檔案、最接近中等策略的可用配置檔案的中位速率配置檔案以及攻擊策略的最高位速率配置檔案開始。 </p> <p>如果指定了最小和最大比特率，則策略在這些速率的約束下工作。 </p> <p> <span class="codeph"> </span> getABRPolicyles會從ABRControlParametersenum返回當 <span class="codeph"> </span> 前設定： <span class="codeph"> ABR_CONSERVATY</span>、 <span class="codeph"> ABR_MODERATE</span>或 <span class="codeph"> ABR_ACCORPISE</span>。 </p> <p>如需詳細資訊，請參閱ABRControlParameters API檔案。</p> </td> 
  </tr> 
 </tbody> 
</table>

請記住下列資訊：

* TVSDK容錯機制可能會覆寫您的設定，因為TVSDK偏好持續播放體驗，而非嚴格遵循您的控制參數。
* 當位元速率變更時，TVSDK會在`PlaybackEventListener`中調度`onProfileChanged`事件。

* 您可以隨時變更ABR設定，而播放器會切換使用最符合最新設定的設定檔。

例如，如果串流具有下列描述檔：

* 1:300000
* 2:700000
* 3:150000
* 4:240000
* 5:400000

如果您指定300000到2000000的範圍，TVSDK只會考慮設定檔1、2和3。 這可讓應用程式因應各種網路狀況進行調整，例如從wi-fi切換至3G或切換至手機、平板電腦或桌上型電腦等各種裝置。

要設定ABR控制參數，請在`ABRControlParameter`類上設定參數。
