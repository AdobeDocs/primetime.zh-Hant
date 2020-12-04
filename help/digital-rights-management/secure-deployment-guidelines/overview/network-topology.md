---
seo-title: 網路拓撲概述
title: 網路拓撲概述
uuid: b8b072dc-8dc0-46ba-bb01-1e9b58af2681
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 概述{#network-topology-overview}

在您成功部署Adobe Primetime DRM後，您必須維護Primetime DRM製作伺服器的安全性。

>[!NOTE]
>
>Primetime DRM之前稱為Adobe Access，之前稱為Flash Access。

您可以使用&#x200B;*反向proxy*&#x200B;來確保Primetime DRM Web應用程式的不同URL集可供外部和內部使用者使用。 *反向* 代理比允許用戶直接連接到運行Primetime DRM的應用伺服器更安全，此配置執行運行Primetime DRM的應用伺服器的所有HTTP請求。使用者只能存取反向代理，且只能嘗試反向代理支援的URL連線。

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)