---
title: 網路層安全
description: 網路層安全
copied-description: true
exl-id: 70c9917d-32bc-43f6-add3-62883f98ac5e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 網路層安全{#network-layer-security}

網路安全漏洞是任何面向Internet或面向Intranet的應用程式伺服器面臨的首批威脅之一。 本節介紹針對這些漏洞加強網路上主機的過程。 它解決了網路分段、傳輸控制協定/Internet協定(TCP/IP)棧加固以及使用防火牆保護主機的問題。

下表介紹了減少網路安全漏洞的常用技術。

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">分段必須至少存在於兩個級別中，應用程式伺服器用於運行位於內部防火牆後面的Adobe訪問。 將外部網路與包含Web伺服器的DMZ分離，而Web伺服器又必須與內部網路分離。 使用防火牆實現分層。 對通過每個網路層的流量進行分類和控制，以確保只允許絕對最小的所需資料。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">專用IP地址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">將網路地址轉換(NAT)與RFC 1918專用IP地址一起使用在Adobe訪問應用程式伺服器上。 分配專用IP地址(10.0.0.0/8 、 172.16.0.0/12和192.168.0.0/16)，使得攻擊者更難通過Internet將流量路由到NAT內部主機和從NAT內部主機路由通信。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火牆 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用以下條件選擇防火牆解決方案： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">實施支援代理伺服器和/或狀態檢查的防火牆，而不是簡單的包過濾解決方案。 </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">使用支援安全范式的防火牆，在該安全范式中，您可以拒絕除明確允許的服務之外的所有服務。 </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">實施雙宿主或多宿主防火牆解決方案。 此體系結構提供了最高級別的安全性，並有助於防止未經授權的用戶繞過防火牆安全性。 </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
