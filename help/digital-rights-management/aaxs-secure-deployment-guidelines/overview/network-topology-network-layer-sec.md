---
title: 網路層安全性
description: 網路層安全性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 網路層安全{#network-layer-security}

網路安全漏洞是對任何面向網際網路或面向內聯網的應用程式伺服器的首批威脅之一。 本節介紹加強網路上主機抵御這些漏洞的過程。 它解決了網路分段、傳輸控制協定/Internet協定(TCP/IP)棧強化以及使用防火牆保護主機的問題。

此表介紹了降低網路安全漏洞的常見技術。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">技術 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非軍事區 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">區段必須至少存在於兩個層級中，而應用程式伺服器用來執行位於內部防火牆後方的Adobe存取。 將外部網路與包含Web伺服器的DMZ分離，而Web伺服器又必須與內部網路分離。 使用防火牆來實現分層。 對流經每個網路層的流量進行分類和控制，以確保僅允許所需資料的絕對最小值。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">專用IP地址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在Adobe訪問應用程式伺服器上，將網路地址轉換(NAT)與RFC 1918專用IP地址一起使用。 指定私有IP位址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使得攻擊者更難以透過網際網路將NAT內部主機的流量路由至網路。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火牆 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用以下標準選擇防火牆解決方案： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">建置支援代理伺服器和／或狀態檢查的防火牆，而非簡單的封包篩選解決方案。 </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">使用支援安全范式的防火牆，您可以拒絕除明確許可之外的所有服務。 </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">實作雙歸屬或多歸屬的防火牆解決方案。 此架構提供最高等級的安全性，並協助防止未經授權的使用者略過防火牆安全性。 </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

