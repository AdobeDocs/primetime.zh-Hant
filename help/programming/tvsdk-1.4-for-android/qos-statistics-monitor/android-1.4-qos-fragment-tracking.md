---
description: 服務品質(QoS)提供視訊引擎執行情形的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。
title: 使用載入資訊在片段層級追蹤
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 使用載入資訊在片段層級追蹤{#track-at-the-fragment-level-using-load-information}

服務品質(QoS)提供視訊引擎執行情形的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。

TVSDK也提供下列下載資源的相關資訊：

1. 播放清單／資訊清單檔案
1. 檔案片段
1. 檔案的追蹤資訊

   您可以從`LoadInfo`類別讀取有關下載資源（如片段和軌道）的服務質量(QoS)資訊。

1. 實作`onLoadInfo`回呼事件偵聽器。
1. 註冊事件偵聽器，TVSDK會在每次片段下載時呼叫該偵聽器。
1. 從傳遞至回呼的`LoadInfo`參數中讀取相關資料。

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
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> <p>下載的持續時間（以毫秒為單位）。 </p> <p>TVSDK不會區分用戶端連線至伺服器的時間與下載完整片段所花的時間。 例如，如果10 MB區段需要8秒才能下載，TVSDK會提供該資訊，但不會告訴您直到第一個位元組再下載4秒，才下載整個片段。 </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> 下載片段的媒體持續時間（以毫秒為單位）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> 與下載的資源相關聯的時間軸期間索引。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 大小  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> 已下載資源的大小（以位元組為單位）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> 相應軌道的索引（如果已知）;否則，為0。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串  </span> </td> 
      <td colname="col2"> 相應軌道的名稱（如果已知）;否則，為null。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串  </span> </td> 
      <td colname="col2"> 相應軌道的類型（如果已知）;否則，為null。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串  </span> </td> 
      <td colname="col2"> TVSDK下載的內容。 下列其中一項： 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST —— 播放清單／資訊清單 </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">片段——片段 </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK —— 與特定軌道關聯的片段 </li> 
      </ul> 有時可能無法檢測資源類型。 如果發生這種情況，則返回FILE。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <span class="codeph"> 字串  </span> </td> 
      <td colname="col2"> 指向已下載資源的URL。 </td> 
      </tr> 
    </tbody> 
   </table>
