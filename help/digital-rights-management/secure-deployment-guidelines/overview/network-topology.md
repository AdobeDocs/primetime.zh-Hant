---
title: 網路拓撲概觀
description: 網路拓撲概觀
copied-description: true
exl-id: a4737ea3-407a-48fd-ae3e-4df56a4c1812
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 概觀 {#network-topology-overview}

成功部署Adobe Primetime DRM後，您必須維護Primetime DRM生產伺服器的安全性。

>[!NOTE]
>
>Primetime DRM先前稱為「Adobe存取」，之前稱為「Flash Access」。

您可以使用 *反向Proxy* 確保外部和內部使用者可以使用Primetime DRM Web應用程式的不同URL集。 *反向Proxy* 比允許使用者直接連線到執行Primetime DRM的應用程式伺服器更安全，而且此組態會針對執行Primetime DRM的應用程式伺服器執行所有HTTP要求。 使用者只能存取反向Proxy，而且只能嘗試反向Proxy支援的URL連線。

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)
