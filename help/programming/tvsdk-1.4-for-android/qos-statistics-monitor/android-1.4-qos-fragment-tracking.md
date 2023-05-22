---
description: 服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 TVSDK提供有關播放、緩衝和設備的詳細統計資訊。
title: 使用負載資訊在片段級別跟蹤
exl-id: 29e82a93-783f-4e32-ab5e-12713a60cfec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 使用負載資訊在片段級別跟蹤{#track-at-the-fragment-level-using-load-information}

服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 TVSDK提供有關播放、緩衝和設備的詳細統計資訊。

TVSDK還提供有關以下下載資源的資訊：

1. 播放清單/清單檔案
1. 檔案片段
1. 檔案跟蹤資訊

   您可以從以下位置讀取有關下載資源（如碎片和軌道）的服務質量(QoS)資訊： `LoadInfo` 類。

1. 實施 `onLoadInfo` 回調事件偵聽器。
1. 註冊事件偵聽器，TVSDK每次下載片段時都會調用該偵聽器。
1. 從 `LoadInfo` 傳遞給回調的參數。

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
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
      <td colname="col1"> <span class="codeph"> 長 </span> </td> 
      <td colname="col2"> <p>下載的持續時間（毫秒）。 </p> <p>TVSDK不區分客戶端連接到伺服器所花的時間和下載完整片段所花的時間。 例如，如果10 MB的段下載需要8秒，則TVSDK會提供該資訊，但不會告訴您下載整個片段需要4秒，直到第一個位元組再花4秒。 </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 媒體持續時間 </span> </td> 
      <td colname="col1"> <span class="codeph"> 長 </span> </td> 
      <td colname="col2"> 下載的片段的媒體持續時間（毫秒）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> 整 </span> </td> 
      <td colname="col2"> 與下載的資源關聯的時間線期間索引。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 大小 </span> </td> 
      <td colname="col1"> <span class="codeph"> 長 </span> </td> 
      <td colname="col2"> 已下載資源的大小（以位元組為單位）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 跟蹤索引 </span> </td> 
      <td colname="col1"> <span class="codeph"> 整 </span> </td> 
      <td colname="col2"> 相應軌道的索引（如果已知）;否則，為0。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 跟蹤名稱 </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串 </span> </td> 
      <td colname="col2"> 相應軌道的名稱（如果已知）;否則，為空。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 跟蹤類型 </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串 </span> </td> 
      <td colname="col2"> 相應軌道的類型（如果已知）;否則，為空。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 類型 </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串 </span> </td> 
      <td colname="col2"> TVSDK下載的內容。 以下情況之一： 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST — 播放清單/清單 </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAGMENT — 片段 </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK — 與特定跟蹤關聯的片段 </li> 
      </ul> 有時，可能無法檢測資源的類型。 如果發生這種情況，則返回FILE。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串 </span> </td> 
      <td colname="col2"> 指向下載資源的URL。 </td> 
      </tr> 
    </tbody> 
   </table>
