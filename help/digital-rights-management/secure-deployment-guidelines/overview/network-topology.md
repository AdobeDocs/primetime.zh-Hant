---
title: 網路拓撲概述
description: 網路拓撲概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 概述{#network-topology-overview}

成功部署Adobe PrimetimeDRM後，您必須維護Primetime DRM製作伺服器的安全性。

>[!NOTE]
>
>Primetime DRM之前稱為Adobe存取，在此之前稱為Flash Access。

您可以使用&#x200B;*反向proxy*&#x200B;來確保Primetime DRM Web應用程式的不同URL集可供外部和內部使用者使用。 *反向* 代理比允許用戶直接連接到運行Primetime DRM的應用伺服器更安全，此配置執行運行Primetime DRM的應用伺服器的所有HTTP請求。使用者只能存取反向代理，且只能嘗試反向代理支援的URL連線。

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)