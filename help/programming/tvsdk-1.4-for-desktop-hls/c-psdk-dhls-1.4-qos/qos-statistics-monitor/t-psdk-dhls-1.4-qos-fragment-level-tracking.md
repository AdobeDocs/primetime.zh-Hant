---
description: 您可以從LoadInformation類讀取有關下載資源（如片段和軌道）的服務質量(QoS)資訊。
seo-description: 您可以從LoadInformation類讀取有關下載資源（如片段和軌道）的服務質量(QoS)資訊。
seo-title: 使用載入資訊在片段層級追蹤
title: 使用載入資訊在片段層級追蹤
uuid: 41fb2b90-3531-4cc5-bf9b-01ccae04d2fd
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 使用載入資訊在片段層級追蹤{#track-at-the-fragment-level-using-load-information}

您可以從LoadInformation類讀取有關下載資源（如片段和軌道）的服務質量(QoS)資訊。

1. 實作回呼 `onLoadInformationAvailable` 事件偵聽器。

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 註冊事件偵聽器，TVSDK會在每次片段下載時呼叫該偵聽器。

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 從傳遞至回呼的 `LoadInformation` 資料中讀取興趣資料。

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> 屬性 </th> 
      <th colname="col1" class="entry"> 類型 </th> 
      <th colname="col2" class="entry"> 說明 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> <p>下載的持續時間（以毫秒為單位）。 </p> <p>TVSDK不會區分用戶端連線至伺服器的時間與下載完整片段所花的時間。 例如，如果10 MB區段需要8秒才能下載，TVSDK會提供該資訊，但不會告訴您直到第一個位元組再下載4秒，才下載整個片段。 </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 下載片段的媒體持續時間（以毫秒為單位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 大小 </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 已下載資源的大小（以位元組為單位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> 相應軌道的索引（如果已知）;否則，為0。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 相應軌道的名稱（如果已知）;否則，為null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 相應軌道的類型（如果已知）;否則，為null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> TVSDK下載的內容。 下列其中一項： 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST —— 播放清單／資訊清單 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">片段——片段 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK —— 與特定軌道關聯的片段 </li> 
      </ul> 有時可能無法檢測資源類型。 如果發生這種情況，則返回FILE。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 指向已下載資源的URL。 </td> 
   </tr> 
   </tbody> 
   </table>
