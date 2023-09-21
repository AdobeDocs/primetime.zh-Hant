---
description: 您可以使用不同的廣告訊號模式和廣告中繼資料組合，標籤、刪除和取代VOD串流中的時間範圍。 訊號模式和中繼資料的不同組合會產生不同的行為。
title: 對從廣告訊號模式和廣告中繼資料組合中插入和刪除廣告的影響
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 對從廣告訊號模式和廣告中繼資料組合中插入和刪除廣告的影響 {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

您可以使用不同的廣告訊號模式和廣告中繼資料組合，標籤、刪除和取代VOD串流中的時間範圍。 訊號模式和中繼資料的不同組合會產生不同的行為。

>[!TIP]
>
>當時間範圍和廣告訊號模式之間發生衝突時，TVSDK會提供時間範圍優先順序。

下表提供有關訊號模式和中繼資料組合行為的詳細資訊：

<table id="table_6044AA1ACFA244FA814EA2D0766C6D12"> 
 <thead> 
  <tr> 
   <th class="entry"> 廣告訊號模式 </th> 
   <th class="entry"> 廣告中繼資料 </th> 
   <th class="entry"> 解析器已建立 </th> 
   <th class="entry"><span class="codeph"> 位置資訊</span> 已建立 </th> 
   <th class="entry"> 產生的行為 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <p><b>伺服器對應</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td> 刪除，Auditude </td> 
   <td> 刪除，Auditude </td> 
   <td> 
    <ul id="ul_E0A2F885E93B4D23A486C37B305E17D8"> 
     <li id="li_D977B398D3904A44AFEC4B05AB0E3340"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)， </span> </li> 
     <li id="li_439886CB38AA46239C2E40352443888A"><span class="codeph"> PlacementInfo (Type.SERVER_MAP， Mode.INSERT)</span> </li> 
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
   <td> 取代，Auditude </td> 
   <td> 刪除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACEMENT)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 已取代範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自訂廣告 </td> 
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
   <td colname="1"> <p><b>資訊清單提示</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td> 刪除，Auditude </td> 
   <td> 刪除，Auditude </td> 
   <td> 
    <ul id="ul_2DD298538E9344B9BAB882485BB57747"> 
     <li id="li_F39A69EFA7ED45C18978A2C462AF7641"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </li> 
     <li id="li_8CCDA3B1C63F4BC396F28F443D8C42F8"><span class="codeph"> PlacementInfo (Type.PRE_ROLL， Mode.INSERT)</span> </li> 
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
   <td> 自訂廣告 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 標示的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 取代，Auditude </td> 
   <td> 刪除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACEMENT)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 已取代範圍 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>自訂時間範圍</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td> 刪除，Auditude </td> 
   <td> 刪除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 刪除範圍，未插入廣告 </td> 
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
   <td> 取代，Auditude </td> 
   <td> 刪除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACEMENT)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 以廣告取代的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自訂廣告 </td> 
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
   <td colname="1"> <p><b>未設定（預設）</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td> 刪除，Auditude </td> 
   <td> 刪除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.INSERT)、PlacementInfo (Type.SERVER_MAP， Mode.DELETE)</span> </td> 
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
   <td> 取代，Auditude </td> 
   <td> 刪除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACEMENT)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 以廣告取代的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自訂廣告 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 標示的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤，Auditude </td> 
   <td> 自訂廣告，Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 標示的範圍 </td> 
  </tr> 
 </tbody> 
</table>
