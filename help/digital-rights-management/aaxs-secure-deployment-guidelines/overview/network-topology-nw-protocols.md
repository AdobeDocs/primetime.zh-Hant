---
title: Adobe存取使用的網路通訊協定
description: Adobe存取使用的網路通訊協定
copied-description: true
exl-id: f065690d-6fa1-43a7-8aa8-a1ccd68e998d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Adobe存取使用的網路通訊協定 {#network-protocols-used-by-adobe-access}

當您設定安全的網路架構時，需要下表中的網路通訊協定，才能在「Adobe存取」與企業網路中的其他系統之間互動。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">通訊協定 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">使用 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player 、 Adobe AIR®和Adobe Primetime使用者端會透過HTTP與Adobe存取通訊。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS （選用） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime使用者端可以使用HTTPS與Adobe存取通訊，不過，除非您需要支援FMRMS 1.x使用者端，否則不需要HTTPS (SSL)。 請參閱表格中的附註 <a href="network-topology-firewall-rules.md" format="dita" scope="local"> 傳入的URL</a> 和 <a href="network-topology-nw-protocols.md"> 設定SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
