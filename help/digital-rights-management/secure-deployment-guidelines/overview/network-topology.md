---
title: 網路拓撲概述
description: 網路拓撲概述
copied-description: true
exl-id: a4737ea3-407a-48fd-ae3e-4df56a4c1812
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 概述 {#network-topology-overview}

成功部署Adobe PrimetimeDRM後，必須維護黃金時段DRM生產伺服器的安全性。

>[!NOTE]
>
>黃金時段DRM以前被稱為Adobe訪問，在此之前是Flash Access。

您可以使用 *反向代理* 確保Mogfire DRM Web應用程式的不同URL集對外部和內部用戶可用。 *反向代理* 比允許用戶直接連接到運行黃金時段DRM的應用伺服器更安全，並且此配置執行運行黃金時段DRM的應用伺服器的所有HTTP請求。 用戶只能訪問反向代理，並且只能嘗試反向代理支援的URL連接。

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)
