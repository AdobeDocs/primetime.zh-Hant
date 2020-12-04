---
seo-title: Adobe Access使用的網路通訊協定
title: Adobe Access使用的網路通訊協定
uuid: 4f2ee3f5-6758-4fbe-b5cd-cead1e5ccde8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Adobe Access {#network-protocols-used-by-adobe-access}使用的網路通訊協定

當您設定安全網路架構時，Adobe Access與企業網路中其他系統之間的互動需要下表中的網路通訊協定。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">協定 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">使用 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR®和Adobe Primetime用戶端可透過HTTP與Adobe Access通訊。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS（可選） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime用戶端可使用HTTPS與Adobe Access通訊，但是，除非您需要支援FMRMS 1.x用戶端，否則不需要HTTPS(SSL)。 請參閱表<a href="network-topology-firewall-rules.md" format="dita" scope="local">傳入URL</a>和<a href="network-topology-nw-protocols.md">設定SSL</a>中的附註。 </p> </td> 
  </tr> 
 </tbody> 
</table>