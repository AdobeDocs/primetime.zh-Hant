---
description: 可以從LoadInformation類讀取有關下載資源（如片段和軌道）的服務質量(QoS)資訊。
title: 使用負載資訊在片段級別跟蹤
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# 使用負載資訊在片段級別跟蹤{#track-at-the-fragment-level-using-load-information}

可以從LoadInformation類讀取有關下載資源（如片段和軌道）的服務質量(QoS)資訊。

1. 實施 `onLoadInformationAvailable` 回調事件偵聽器。

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 註冊事件偵聽器，TVSDK每次下載片段時都會調用該偵聽器。

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 從 `LoadInformation` 傳給回叫的。

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
      <td colname="col01"> <span class="codeph"> 下載持續時間 </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> <p>下載的持續時間（毫秒）。 </p> <p>TVSDK不區分客戶端連接到伺服器所花的時間和下載完整片段所花的時間。 例如，如果10 MB的段下載需要8秒，則TVSDK會提供該資訊，但不會告訴您下載整個片段需要4秒，直到第一個位元組再花4秒。 </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 媒體持續時間 </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 下載的片段的媒體持續時間（毫秒）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 大小 </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 已下載資源的大小（以位元組為單位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 跟蹤索引 </span> </td> 
      <td colname="col1"> <p>整 </p> </td> 
      <td colname="col2"> 相應軌道的索引（如果已知）;否則，為0。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 跟蹤名稱 </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 相應軌道的名稱（如果已知）;否則，為空。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 跟蹤類型 </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 相應軌道的類型（如果已知）;否則，為空。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 類型 </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> TVSDK下載的內容。 以下情況之一： 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST — 播放清單/清單 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAGMENT — 片段 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK — 與特定跟蹤關聯的片段 </li> 
      </ul> 有時，可能無法檢測資源的類型。 如果發生這種情況，則返回FILE。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 指向下載資源的URL。 </td> 
   </tr> 
   </tbody> 
   </table>
