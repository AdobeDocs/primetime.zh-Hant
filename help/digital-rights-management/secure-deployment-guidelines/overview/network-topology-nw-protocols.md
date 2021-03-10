---
description: 配置安全網路體系結構時，在Adobe PrimetimeDRM與企業網路中的其他系統之間交互時，需要網路協定。
title: Adobe PrimetimeDRM網路協定
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Adobe PrimetimeDRM網路協定{#adobe-primetime-drm-network-protocols}

配置安全網路體系結構時，在Adobe PrimetimeDRM與企業網路中的其他系統之間交互時，需要網路協定。

配置安全網路體系結構時，此交互需要以下網路協定：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">協定 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">使用 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR®和Adobe Primetime用戶端透過HTTP與Primetime DRM通訊。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS（可選） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime用戶端可使用HTTPS與Primetime DRM通訊；除非您支援FMRMS 1.x用戶端，否則不需要HTTPS(SSL)。 如需詳細資訊，請參閱<a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local">傳入URL </a>和設定SSL。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 應用程式伺服器{#ports-for-application-servers}的埠

您可以配置Adobe PrimetimeDRM許可證伺服器以使用任何網路埠。

這些埠必須在內部防火牆上啟用或禁用，具體取決於要允許連接到運行Primetime DRM的應用程式伺服器的客戶端的網路功能。

## 配置SSL {#configuring-ssl}

只有在需要支援Flash媒體Rights Management伺服器1.x客戶端時，才需要安全套接字層(SSL)。

Adobe PrimetimeDRM密鑰伺服器需要具有客戶端驗證的SSL。 有關詳細資訊，請參閱[使用Adobe PrimetimeDRM密鑰伺服器](../../using-the-drm-key-server/requirements.md)。