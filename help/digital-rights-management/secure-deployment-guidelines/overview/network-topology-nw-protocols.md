---
description: 當您設定安全的網路架構時，Adobe Primetime DRM與企業網路中其他系統之間的互動需要網路通訊協定。
title: Adobe Primetime DRM網路通訊協定
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Adobe Primetime DRM網路通訊協定 {#adobe-primetime-drm-network-protocols}

當您設定安全的網路架構時，Adobe Primetime DRM與企業網路中其他系統之間的互動需要網路通訊協定。

當您設定安全的網路架構時，此互動需要下列網路通訊協定：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">通訊協定 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">使用 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR®和Adobe Primetime使用者端會透過HTTP與Primetime DRM通訊。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS （選用） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime使用者端可使用HTTPS與Primetime DRM通訊；除非您支援FMRMS 1.x使用者端，否則不需要HTTPS (SSL)。 如需詳細資訊，請參閱 <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> 傳入URL </a> 和設定SSL。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 應用程式伺服器的連線埠 {#ports-for-application-servers}

您可以設定Adobe Primetime DRM授權伺服器使用任何網路連線埠。

這些連線埠必須在內部防火牆上啟用或停用，這取決於您要允許連線到執行Primetime DRM的應用程式伺服器的使用者端使用的網路功能。

## 設定SSL {#configuring-ssl}

只有在您需要支援Flash MediaRights Management伺服器1.x使用者端時，才需要安全通訊端層(SSL)。

Adobe Primetime DRM金鑰伺服器需要具有使用者端驗證的SSL。 如需詳細資訊，請參閱 [使用Adobe Primetime DRM Key Server](../../using-the-drm-key-server/requirements.md).
