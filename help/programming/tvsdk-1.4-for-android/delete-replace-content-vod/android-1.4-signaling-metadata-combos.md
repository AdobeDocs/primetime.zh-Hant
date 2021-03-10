---
description: 您可以使用不同的廣告信令模式和廣告中繼資料組合來標籤、刪除和取代VOD串流中的時間範圍。 不同的信令模式和元資料組合導致不同的行為。
title: 從廣告信號模式和廣告中繼資料組合中對廣告插入和刪除的影響
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# 從廣告信號模式和廣告中繼資料組合中插入和刪除廣告的效果{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

您可以使用不同的廣告信令模式和廣告中繼資料組合來標籤、刪除和取代VOD串流中的時間範圍。 不同的信令模式和元資料組合導致不同的行為。

>[!NOTE]
>
>當時間範圍與廣告信令模式發生衝突時，TVSDK會給予時間範圍優先順序。

**表3:信令模式／中繼資料組合行為**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> 廣告信令模式 </th> 
   <th class="entry"> 廣告中繼資料 </th> 
   <th class="entry"> 已建立解析器 </th> 
   <th class="entry"><span class="codeph"> 位置</span> 資訊建立 </th> 
   <th class="entry"> 結果行為 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>伺服器地圖</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除， Auditude </td> 
   <td> 刪除， Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
     <li><span class="codeph"> PlacementInfo(Type.SERVER_MAP,Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 刪除範圍，插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP,Mode.INSERT)</span> </td> 
   <td> 插入的廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 取代，Auditude </td> 
   <td> 刪除， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE、Mode.REPLACE)</span> </td> 
   <td> 已取代範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自訂廣告 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤範圍，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td> <b>資訊清單提示</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> 插入的廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除， Auditude </td> 
   <td> 刪除， Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo(Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 刪除範圍，插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Mark, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤範圍，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自訂廣告 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 取代，Auditude </td> 
   <td> 刪除， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE、Mode.REPLACE)</span> </td> 
   <td> 已取代範圍 </td> 
  </tr> 
  <tr> 
   <td> <b>自訂時間範圍</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除， Auditude </td> 
   <td> 刪除， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> 無 </td> 
   <td> 未插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 取代，Auditude </td> 
   <td> 刪除， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE、Mode.REPLACE)</span> </td> 
   <td> 以廣告取代範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自訂廣告 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> 自訂廣告、Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤範圍，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td> <b>未設定（預設）</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除， Auditude </td> 
   <td> 刪除， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> 刪除範圍，插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP,Mode.INSERT)</span> </td> 
   <td> 插入的廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 取代，Auditude </td> 
   <td> 刪除， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE、Mode.REPLACE)</span> </td> 
   <td> 以廣告取代範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自訂廣告 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
 </tbody> 
</table>

