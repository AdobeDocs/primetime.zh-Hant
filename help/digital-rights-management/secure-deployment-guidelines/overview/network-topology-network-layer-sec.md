---
description: 網路安全漏洞是對面向網際網路或面向內聯網的應用程式伺服器的首要威脅之一，您必須針對這些漏洞加強網路上的主機。
title: 網路層安全性
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# 網路層安全{#network-layer-security}

網路安全漏洞是對面向網際網路或面向內聯網的應用程式伺服器的首要威脅之一，您必須針對這些漏洞加強網路上的主機。

以下是一些降低網路安全漏洞的常見技術：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">技術 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非軍事區 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">當Primetime DRM位於內部防火牆後方時，區段必須存在於應用程式伺服器的至少兩個層級中，該應用程式伺服器用來執行Adobe PrimetimeDRM。 您必須將外部網路與包含Web伺服器的DMZ分離，並且Web伺服器必須與內部網路分離。 您可以使用防火牆來建置這些隔離層。 </p> <p>您可以分類並控制通過每個網路層的流量，以確保僅允許絕對最小的所需資料。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">專用IP地址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在Primetime DRM應用伺服器上，將網路地址轉換(NAT)與RFC 1918專用IP地址一起使用。 您可以指派私有IP位址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使得攻擊者更難以透過網際網路將NAT內部主機的流量路由至網路。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火牆 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">以下是選擇防火牆解決方案時要考慮的一些標準： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">建置支援代理伺服器和／或狀態檢查的防火牆，而非簡單的封包篩選解決方案。 </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">使用防火牆來支援安全范式，您可以拒絕所有服務，但明確許可的服務除外。 </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">實作雙歸屬或多歸屬的防火牆解決方案。 此架構提供最高等級的安全性，並防止未經授權的使用者略過防火牆安全性。 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

