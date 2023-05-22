---
description: 網路安全漏洞是面向Internet或面向Intranet的應用程式伺服器面臨的首批威脅之一，您必須針對這些漏洞加強網路上的主機。
title: 網路層安全
exl-id: 0a45d18a-66aa-4ecc-8eaf-e2af599eb3b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 網路層安全{#network-layer-security}

網路安全漏洞是面向Internet或面向Intranet的應用程式伺服器面臨的首批威脅之一，您必須針對這些漏洞加強網路上的主機。

以下是一些減少網路安全漏洞的常用技術：

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">當Migna時DRM位於內部防火牆後面時，使用運行Adobe PrimetimeDRM的應用程式伺服器至少必須存在兩個級別的分段。 您必須將外部網路與包括Web伺服器的DMZ分離，並且Web伺服器必須與內部網路分離。 您可以使用防火牆來實現這些層次的隔離。 </p> <p>您可以對通過每個網路層的通信量進行分類和控制，以確保只允許絕對最小的所需資料。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">專用IP地址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在黃金時段DRM應用伺服器上，將網路地址轉換(NAT)與RFC 1918專用IP地址一起使用。 您可以分配專用IP地址(10.0.0.0/8 、 172.16.0.0/12和192.168.0.0/16)，使得攻擊者更難通過Internet將流量路由到NAT內部主機和從NAT內部主機發送流量。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火牆 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">以下是選擇防火牆解決方案時要考慮的一些標準： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">實施支援代理伺服器和/或狀態檢查的防火牆，而不是簡單的包過濾解決方案。 </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">使用支援安全范式的防火牆，在該安全范式中，您可以拒絕除明確允許的服務之外的所有服務。 </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">實施雙宿主或多宿主防火牆解決方案。 此體系結構提供了最高級別的安全性，並防止未經授權的用戶繞過防火牆安全性。 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
