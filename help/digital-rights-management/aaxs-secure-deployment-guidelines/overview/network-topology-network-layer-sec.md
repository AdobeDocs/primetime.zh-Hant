---
title: 網路層安全性
description: 網路層安全性
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 網路層安全性{#network-layer-security}

網路安全漏洞是任何面對網際網路或面對內部網路的應用程式伺服器所面臨的首要威脅之一。 本節說明針對這些弱點強化網路上主機的程式。 它可處理網路細分、傳輸控制通訊協定/網際網路通訊協定(TCP/IP)棧疊強化，以及使用防火牆保護主機等問題。

此表格說明減少網路安全漏洞的常用技術。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">技術 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非軍事區域(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">區段必須至少存在於兩個層級，而且用來執行Adobe存取的應用程式伺服器必須置於內部防火牆之後。 將外部網路與包含Web伺服器的DMZ分開，而後者則必須與內部網路分開。 使用防火牆來實作分隔層。 將流經每個網路層的流量分類並加以控制，確保只允許絕對最低必要資料。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">私人IP位址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在Adobe Access應用程式伺服器上使用網路位址轉譯(NAT)搭配RFC 1918私人IP位址。 指派私人IP位址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，讓攻擊者更難以透過網際網路路由往來於NAT內部主機的流量。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火牆 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">請使用下列條件來選取防火牆解決方案： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">實作支援Proxy伺服器及/或狀態檢查（而非簡單的封包篩選解決方案）的防火牆。 </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">使用支援安全範例的防火牆，您可以拒絕所有服務，但明確允許的除外。 </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">實作雙主機或多主機防火牆解決方案。 此架構提供最高層級的安全性，並有助於防止未經授權的使用者繞過防火牆安全性。 </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
