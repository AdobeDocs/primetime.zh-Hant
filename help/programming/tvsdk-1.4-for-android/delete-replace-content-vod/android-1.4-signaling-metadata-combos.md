---
description: 您可以使用不同的廣告訊號模式和廣告中繼資料組合，標籤、刪除和取代VOD串流中的時間範圍。 訊號模式和中繼資料的不同組合會產生不同的行為。
title: 對從廣告訊號模式和廣告中繼資料組合中插入和刪除廣告的影響
exl-id: 0b265471-2d5c-432b-b1c9-c850ce99f2f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 對從廣告訊號模式和廣告中繼資料組合中插入和刪除廣告的影響{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

您可以使用不同的廣告訊號模式和廣告中繼資料組合，標籤、刪除和取代VOD串流中的時間範圍。 訊號模式和中繼資料的不同組合會產生不同的行為。

>[!NOTE]
>
>當時間範圍和廣告訊號模式之間發生衝突時，TVSDK會提供時間範圍優先順序。

**表3：訊號模式/中繼資料組合行為**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> 廣告訊號模式 </th> 
   <th class="entry"> 廣告中繼資料 </th> 
   <th class="entry"> 解析器已建立 </th> 
   <th class="entry"><span class="codeph"> PlacementInformations</span> 已建立 </th> 
   <th class="entry"> 產生的行為 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>伺服器對應</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除，稽核 </td> 
   <td> 刪除，稽核 </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)， </span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.SERVER_MAP， Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 刪除範圍，插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP， Mode.INSERT)</span> </td> 
   <td> 廣告已插入 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 取代，稽核 </td> 
   <td> 刪除，稽核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 範圍已取代 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 標示的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤，Auditude </td> 
   <td> CustomAd， Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 已標籤範圍，未插入廣告 </td> 
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
   <td><span class="codeph"> PlacementInfo (Type.PRE_ROLL， Mode.INSERT)</span> </td> 
   <td> 廣告已插入 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除，稽核 </td> 
   <td> 刪除，稽核 </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.PRE_ROLL， Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 刪除範圍，插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤，Auditude </td> 
   <td> 標籤，Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 已標籤範圍，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 標示的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 取代，稽核 </td> 
   <td> 刪除，稽核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 範圍已取代 </td> 
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
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除，稽核 </td> 
   <td> 刪除，稽核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 範圍已刪除，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> 無 </td> 
   <td> 未插入任何廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 取代，稽核 </td> 
   <td> 刪除，稽核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 範圍已取代為廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 標示的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤，Auditude </td> 
   <td> 自訂廣告，Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 已標籤範圍，未插入廣告 </td> 
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
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除，稽核 </td> 
   <td> 刪除，稽核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.INSERT)、PlacementInfo (Type.SERVER_MAP， Mode.INSERT)DELETE</span> </td> 
   <td> 刪除範圍，插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP， Mode.INSERT)</span> </td> 
   <td> 廣告已插入 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 取代，稽核 </td> 
   <td> 刪除，稽核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 範圍已取代為廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 標示的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤，Auditude </td> 
   <td> CustomAd， Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 標示的範圍 </td> 
  </tr> 
 </tbody> 
</table>
