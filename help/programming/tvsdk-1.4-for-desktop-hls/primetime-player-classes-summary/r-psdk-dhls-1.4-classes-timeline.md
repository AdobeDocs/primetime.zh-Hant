---
description: 這些類別提供有關特定媒體時間軸的資訊，包括廣告的刊登。
title: 時間表類別
exl-id: 8382fff2-0f10-4a8c-9c0c-66d26fe18938
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
   <td colname="2"> 定義通訊協定的介面，當您想要建立旨在與TVSDK程式庫整合的內容追蹤模組時，必須實作此介面。 <p>此介面需要您定義向遠端追蹤系統報告進度事件的方式。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> 機會 </a> </span> </td> 
   <td colname="2"> 所有機會類別的基底類別。 機會類別代表時間軸上的「有趣」點。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> 刊登 </a> </span> </td> 
   <td colname="2"> 封裝與時間表位置相關資訊的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> PlacementMode </a> </span> </td> 
   <td colname="2"> 版位模式的列舉，例如，是否要插入或取代內容。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType </a> </span> </td> 
   <td colname="2"> 表示在時間軸中放置位置的放置型別列舉；例如PRE_ROLL。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> 預訂 </a> </span> </td> 
   <td colname="2"> 預約可用於限制或防止進一步處理時間表上的特定時間範圍。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> 時間表 </a> </span> </td> 
   <td colname="2"> 提供處理時間軸標籤迭代器的介面。 代表內容的時間軸，包括廣告插播。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> 時間軸專案 </a> </span> </td> 
   <td colname="2"> 類別。 時間表專案的一般不可變表示。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> 時間軸標籤 </a> </span> </td> 
   <td colname="2"> 代表時間軸上標籤的類別。 這會在實際時間軸上標籤感興趣的區域。 目前，感興趣的地區是廣告，您可能會想要以不同的顏色在拖曳列UI上加以標籤。 每個標籤都由位置和持續時間（每個均以毫秒表示）定義。 </td> 
  </tr> 
 </tbody> 
</table>
