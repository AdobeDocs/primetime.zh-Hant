---
description: 這些類提供關於特定媒體的時間表的資訊，包括廣告的放置。
title: 時間軸類
exl-id: 8382fff2-0f10-4a8c-9c0c-66d26fe18938
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 時間軸類{#timeline-classes}

這些類提供關於特定媒體的時間表的資訊，包括廣告的放置。

包： [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名稱 </th> 
   <th colname="2" class="entry"> <p>說明 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> 內容跟蹤器 </a> </span> </td> 
   <td colname="2"> 介面，用於定義要建立內容跟蹤模組以與TVSDK庫整合時必須實現的協定。 <p>此介面要求您定義向遠程跟蹤系統報告進度事件的方式。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> 機會 </a> </span> </td> 
   <td colname="2"> 所有機會類的基類。 機會類表示時間線上的「有趣」點。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> 放置 </a> </span> </td> 
   <td colname="2"> 封裝與時間軸放置相關資訊的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> 放置模式 </a> </span> </td> 
   <td colname="2"> 列出放置模式，如插入或替換內容。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> 放置類型 </a> </span> </td> 
   <td colname="2"> 列出表示在時間線中放置的位置的放置類型；例如，PRE_ROLL。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> 保留 </a> </span> </td> 
   <td colname="2"> 使用保留來限制或阻止對時間線上的特定時間範圍的進一步處理。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> 時間軸 </a> </span> </td> 
   <td colname="2"> 提供迭代器以處理時間軸標籤的介面。 表示內容的時間線，包括廣告分段。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> 時間軸項 </a> </span> </td> 
   <td colname="2"> 課。 時間軸項的通用不可變表示。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> 時間軸標籤 </a> </span> </td> 
   <td colname="2"> 表示時間軸上標籤的類。 這標籤實際時間線上感興趣的區域。 當前，感興趣的區域是廣告，例如，您可能希望在擦洗條UI上用不同顏色標籤這些廣告。 每個標籤由位置和持續時間（每個以毫秒錶示）定義。 </td> 
  </tr> 
 </tbody> 
</table>
