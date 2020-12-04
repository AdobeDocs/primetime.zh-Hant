---
description: 當您設定安全的網路架構時，Adobe Primetime DRM與企業網路中其他系統之間的互動需要網路通訊協定。
seo-description: 當您設定安全的網路架構時，Adobe Primetime DRM與企業網路中其他系統之間的互動需要網路通訊協定。
seo-title: Adobe Primetime DRM網路通訊協定
title: Adobe Primetime DRM網路通訊協定
uuid: 8954e33c-83ac-4b40-9e45-005d4954b44e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Adobe Primetime DRM網路通訊協定{#adobe-primetime-drm-network-protocols}

當您設定安全的網路架構時，Adobe Primetime DRM與企業網路中其他系統之間的互動需要網路通訊協定。

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

您可以設定Adobe Primetime DRM授權伺服器以使用任何網路埠。

這些埠必須在內部防火牆上啟用或禁用，具體取決於要允許連接到運行Primetime DRM的應用程式伺服器的客戶端的網路功能。

## 配置SSL {#configuring-ssl}

只有在您需要支援Flash Media Rights Management Server 1.x用戶端時，才需要安全通訊端層(SSL)。

Adobe Primetime DRM金鑰伺服器需要具備用戶端驗證的SSL。 如需詳細資訊，請參閱[使用Adobe Primetime DRM Key Server](../../using-the-drm-key-server/requirements.md)。