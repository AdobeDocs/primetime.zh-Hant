---
description: HLS和DASH串流針對相同的視訊短脈衝串提供不同的位元速率編碼（描述檔）。 瀏覽器TVSDK可根據可用頻寬來選取每個突發串的品質等級。
seo-description: HLS和DASH串流針對相同的視訊短脈衝串提供不同的位元速率編碼（描述檔）。 瀏覽器TVSDK可根據可用頻寬來選取每個突發串的品質等級。
seo-title: 視訊品質的可調式位元速率(ABR)
title: 視訊品質的可調式位元速率(ABR)
uuid: 4c34fb7b-1bbd-4fa9-8929-d50e85a17396
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---


# 概述{#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH串流針對相同的視訊短脈衝串提供不同的位元速率編碼（描述檔）。 瀏覽器TVSDK可根據可用頻寬來選取每個突發串的品質等級。

瀏覽器TVSDK會持續監視位元速率，以確保內容以目前網路連線的最佳位元速率播放。

您可以為多位速率(MBR)串流設定自適應位速率(ABR)切換策略和初始、最小和最大位速率。 瀏覽器TVSDK會自動切換至位元速率，以在指定組態中提供最佳播放體驗。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位元速率 </td> 
   <td colname="col2">第一段的所需播放位速率（以位／秒為單位）。 當播放開始時，第一個區段會使用最接近的描述檔，該描述檔等於或大於初始位元速率。 <p> 如果定義了最小位元速率，且初始位元速率低於最小速率，則瀏覽器TVSDK會選擇位元速率高於最小位元速率的描述檔。 如果初始速率高於最大速率，瀏覽器TVSDK會選擇低於最大速率的最高速率。 </p> <p>如果初始比特率為零或未定義，則初始比特率由ABR策略確定。 </p> <p><span class="codeph"> initialBitRate</span> 會傳回一個整數值，代表每秒位元組描述檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最低位元速率 </td> 
   <td colname="col2">ABR可切換至的最低允許位速率。 ABR切換會忽略位速率低於此位速率的描述檔。 <p><span class="codeph"> </span> minBitRate會傳回一個整數值，代表每秒位元描述檔。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大位元速率 </td> 
   <td colname="col2">ABR可切換的最高允許位速率。 ABR切換會忽略位速率高於此位速率的描述檔。 <p><span class="codeph"> </span> maxBitRate會傳回一個整數值，代表每秒位元描述檔。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住下列資訊：

* 當位元速率變更時，Browser TVSDK會以`AdobePSDK.PSDKEventType.PROFILE_CHANGED`的類型分派`AdobePSDK.ProfileEvent`。

* 您可以隨時變更ABR設定，而播放器會切換使用最符合最新設定的設定檔。

例如，如果串流具有下列描述檔：

* 1:300000
* 2:700000
* 3:150000
* 4:240000
* 5:400000

如果您指定300000到2000000的範圍，瀏覽器TVSDK只會考慮設定檔1、2和3。 這可讓應用程式因應各種網路狀況進行調整，例如從wi-fi切換至3G或切換至手機、平板電腦或桌上型電腦等各種裝置。

要設定ABR控制參數，請執行以下操作：

* 在`ABRControlParameters`類中設定參數。

