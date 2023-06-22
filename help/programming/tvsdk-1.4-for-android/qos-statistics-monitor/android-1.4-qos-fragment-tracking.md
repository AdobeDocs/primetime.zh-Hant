---
description: 服務品質(QoS)提供視訊引擎執行狀況的詳細檢視。 TVSDK提供有關播放、緩衝和裝置的詳細統計資料。
title: 使用載入資訊在片段層級追蹤
exl-id: 29e82a93-783f-4e32-ab5e-12713a60cfec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 使用載入資訊在片段層級追蹤{#track-at-the-fragment-level-using-load-information}

服務品質(QoS)提供視訊引擎執行狀況的詳細檢視。 TVSDK提供有關播放、緩衝和裝置的詳細統計資料。

TVSDK也提供下列已下載資源的相關資訊：

1. 播放清單/資訊清單檔案
1. 檔案片段
1. 檔案的追蹤資訊

   您可以閱讀服務品質(QoS)資訊，瞭解下載的資源，例如片段和曲目，網址為 `LoadInfo` 類別。

1. 實作 `onLoadInfo` 回呼事件監聽器。
1. 註冊事件監聽器，TVSDK在每次下載片段時都會呼叫此監聽器。
1. 從讀取感興趣的資料 `LoadInfo` 傳遞至回呼的引數。

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
    <thead> 
      <tr> 
      <th colname="col01" class="entry"> 屬性 </th> 
      <th colname="col1" class="entry"> 型別 </th> 
      <th colname="col2" class="entry"> 說明 </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col01"> <span class="codeph"> downloadduration </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> <p>下載持續時間（毫秒）。 </p> <p>TVSDK不會區分使用者端連線至伺服器所花的時間與下載完整片段所花的時間。 例如，如果下載10 MB的區段需要8秒，TVSDK會提供該資訊，但不會告訴您直到第一個位元組花了4秒，然後又花了4秒來下載整個片段。 </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> 下載片段的媒體持續時間（毫秒）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodindex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> 與下載的資源關聯的時間軸期間索引。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 大小 </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> 已下載資源的大小（位元組）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> 對應曲目的索引（如果已知）；否則為0。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串 </span> </td> 
      <td colname="col2"> 對應曲目的名稱（如果已知）；否則為null。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串 </span> </td> 
      <td colname="col2"> 對應曲目的型別（如果已知）；否則為null。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串 </span> </td> 
      <td colname="col2"> 下載的TVSDK。 下列其中一項： 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">資訊清單 — 播放清單/資訊清單 </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">片段 — 片段 </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK — 與特定曲目相關聯的片段 </li> 
      </ul> 有時可能無法偵測資源的型別。 如果發生此情況，則會傳回FILE。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串 </span> </td> 
      <td colname="col2"> 指向已下載資源的URL。 </td> 
      </tr> 
    </tbody> 
   </table>
