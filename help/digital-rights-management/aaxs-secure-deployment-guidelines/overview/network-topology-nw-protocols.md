---
title: Adobe訪問使用的網路協定
description: Adobe訪問使用的網路協定
copied-description: true
exl-id: f065690d-6fa1-43a7-8aa8-a1ccd68e998d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Adobe訪問使用的網路協定 {#network-protocols-used-by-adobe-access}

配置安全網路體系結構時，Adobe訪問與企業網路中其他系統之間的交互需要下表中的網路協定。

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR®和Adobe Primetime客戶端通過HTTP與Adobe訪問通信。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS（可選） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime客戶端可以使用HTTPS與Adobe訪問通信，但是，除非您需要FMRMS 1.x客戶端的支援，否則不需要HTTPS(SSL)。 請參閱表中的注釋 <a href="network-topology-firewall-rules.md" format="dita" scope="local"> 傳入URL</a> 和 <a href="network-topology-nw-protocols.md"> 配置SSL</a>。 </p> </td> 
  </tr> 
 </tbody> 
</table>
