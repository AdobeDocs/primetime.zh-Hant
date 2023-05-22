---
description: HLS和DASH流為同一短視頻突發提供不同的比特率編碼（簡檔）。 瀏覽器TVSDK可以根據可用頻寬為每個突發選擇質量級別。
title: 用於視頻質量的自適應比特率(ABR)
exl-id: 2506a57b-d77d-4bd1-9e4c-5e00ef1bc8b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# 概述 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH流為同一短視頻突發提供不同的比特率編碼（簡檔）。 瀏覽器TVSDK可以根據可用頻寬為每個突發選擇質量級別。

瀏覽器TVSDK持續監視比特率以確保以當前網路連接的最佳比特率播放內容。

可以為多比特率(MBR)流設定自適應比特率(ABR)切換策略以及初始、最小和最大比特率。 瀏覽器TVSDK自動切換到在指定配置中提供最佳回放體驗的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2">第一段的所需重放比特率（以位/秒為單位）。 當播放開始時，最接近的輪廓（等於或大於初始比特率）用於第一段。 <p> 如果定義了最小比特率並且初始比特率低於最小速率，則瀏覽器TVSDK選擇具有高於最小比特率的最低比特率的配置檔案。 如果初始速率高於最大速率，則瀏覽器TVSDK將選擇低於最大速率的最高速率。 </p> <p>如果初始比特率為零或未定義，則初始比特率由ABR策略確定。 </p> <p><span class="codeph"> 初始比特率</span> 返回表示每秒位元組配置檔案的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2">ABR可切換到的最低允許比特率。 ABR切換忽略比此比特率更低的比特率的簡檔。 <p><span class="codeph"> 最小比特率</span> 返回表示每秒位配置檔案的整數值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2">ABR可切換到的最高允許比特率。 ABR切換忽略比此比特率更高的比特率的簡檔。 <p><span class="codeph"> 最大比特率</span> 返回表示每秒位配置檔案的整數值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請牢記以下資訊：

* 當比特率更改時，Browser TVSDK派單 `AdobePSDK.ProfileEvent` 類型為 `AdobePSDK.PSDKEventType.PROFILE_CHANGED`。

* 您可以隨時更改ABR設定，播放器會切換使用與最近設定最接近的配置式。

例如，如果流具有以下配置檔案：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定範圍為300000到2000000，則Browser TVSDK僅考慮配置檔案1、2和3。 這允許應用程式根據各種網路條件進行調整，例如從wi-fi切換到3G或切換到各種設備，如電話、平板或台式電腦。

要設定ABR控制參數：

* 在 `ABRControlParameters` 類。
