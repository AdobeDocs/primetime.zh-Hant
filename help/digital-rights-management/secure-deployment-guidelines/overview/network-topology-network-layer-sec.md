---
description: 網路安全漏洞是任何面對網際網路或面對內部網路的應用程式伺服器所面臨的首要威脅之一，您必須加強網路上的主機以防範這些漏洞。
title: 網路層安全性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 網路層安全性{#network-layer-security}

網路安全漏洞是任何面對網際網路或面對內部網路的應用程式伺服器所面臨的首要威脅之一，您必須加強網路上的主機以防範這些漏洞。

以下是一些減少網路安全漏洞的常見技術：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">技術 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非軍事區域(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">當Primetime DRM位於內部防火牆後面時，使用執行Adobe Primetime DRM之應用程式伺服器的區段必須至少存在於兩個層級。 您必須將外部網路與包含Web伺服器的DMZ分開，且Web伺服器必須與內部網路分開。 您可以使用防火牆來實作這些分隔層。 </p> <p>您可以分類和控制流經每個網路層的流量，以確保只允許絕對最小的必要資料。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">私人IP位址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在Primetime DRM應用程式伺服器上使用網路位址轉譯(NAT)搭配RFC 1918私人IP位址。 您可以指派私人IP位址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，讓攻擊者更難以透過網際網路路由往來於NAT內部主機的流量。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火牆 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">以下是選取防火牆解決方案時應考量的一些准則： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">實作支援Proxy伺服器及/或狀態檢查的防火牆，而非簡單的封包篩選解決方案。 </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">使用支援安全性範例的防火牆，您可以拒絕所有服務，但明確允許的服務除外。 </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">實作雙主機或多主機防火牆解決方案。 此架構提供最高層級的安全性，並防止未經授權的使用者繞過防火牆安全性。 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
