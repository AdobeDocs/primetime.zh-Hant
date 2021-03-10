---
description: 這些類別提供特定媒體時間軸的相關資訊，包括廣告的放置。
title: 時間軸課程
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# 時間軸類{#timeline-classes}

這些類別提供特定媒體時間軸的相關資訊，包括廣告的放置。

套件：[com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名稱 </th> 
   <th colname="2" class="entry"> <p>說明 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker  </a> </span> </td> 
   <td colname="2"> 定義您若要建立內容追蹤模組以與TVSDK程式庫整合時必須實作之通訊協定的介面。 <p>此介面要求您定義向遠端追蹤系統報告進度事件的方式。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> 機會  </a> </span> </td> 
   <td colname="2"> 所有機會類的基類。 機會類別代表時間軸上的「有趣」點。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> 位置  </a> </span> </td> 
   <td colname="2"> 包住與時間軸放置相關資訊的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> 放置模式  </a> </span> </td> 
   <td colname="2"> 列舉放置模式，例如插入或取代內容。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType  </a> </span> </td> 
   <td colname="2"> 列出表示在時間軸中放置的位置的放置類型；例如PRE_ROLL。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> 保留  </a> </span> </td> 
   <td colname="2"> 使用保留來限制或阻止對時間軸上的特定時間範圍的進一步處理。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> 時間軸  </a> </span> </td> 
   <td colname="2"> 介面，提供處理時間軸標籤的迭代器。 代表內容的時間軸，包括廣告插播。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> TimelineItem  </a> </span> </td> 
   <td colname="2"> 類別。 時間軸項的通用不可變表示法。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> TimelineMarker  </a> </span> </td> 
   <td colname="2"> 表示時間軸上標籤的類。 這會標示實際時間軸上感興趣的區域。 目前，感興趣的區域是廣告，例如，您可能想要在拖曳列UI上以不同的顏色標籤廣告。 每個標籤都由位置和持續時間定義（每個以毫秒錶示）。 </td> 
  </tr> 
 </tbody> 
</table>

