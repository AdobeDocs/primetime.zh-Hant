---
description: 這些類別提供有關特定媒體時間軸的資訊，包括廣告的刊登。
title: 時間表類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 時間表類別{#timeline-classes}

這些類別提供有關特定媒體時間軸的資訊，包括廣告的刊登。

封裝： [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名稱 </th> 
   <th colname="2" class="entry"> <p>說明 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker </a> </span> </td> 
   <td colname="2"> 定義您必須實作的通訊協定介面，以建立旨在與TVSDK程式庫整合的內容追蹤模組。 <p>此介面需要您定義向遠端追蹤系統報告進度事件的方式。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> 商機 </a> </span> </td> 
   <td colname="2"> 所有機會類別的基底類別。 機會類別代表時間表上的「有趣」點。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> 刊登 </a> </span> </td> 
   <td colname="2"> 封裝與時間表位置相關資訊的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> 放置模式 </a> </span> </td> 
   <td colname="2"> 版位模式的列舉，例如，是否要插入或取代內容。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType </a> </span> </td> 
   <td colname="2"> 表示在時間軸中放置位置的放置型別列舉；例如PRE_ROLL。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> 預訂 </a> </span> </td> 
   <td colname="2"> 預訂可用於限制或防止在時間線上進一步處理特定時間範圍。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> 時間表 </a> </span> </td> 
   <td colname="2"> 提供處理時間軸標籤之迭代器的介面。 代表內容的時間軸，包括廣告插播。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> 時間軸專案 </a> </span> </td> 
   <td colname="2"> 類別。 時間表專案的一般不可變表示法。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> 時間軸標籤 </a> </span> </td> 
   <td colname="2"> 代表時間軸上標籤的類別。 這會在實際時間表上標示感興趣的區域。 目前，感興趣的區域是廣告，您可能會想要以不同的顏色在拖曳列UI上加以標籤。 每個標籤由位置和持續時間（每個以毫秒表示）定義。 </td> 
  </tr> 
 </tbody> 
</table>
