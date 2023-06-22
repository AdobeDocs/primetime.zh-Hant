---
title: 網路拓撲概觀
description: 網路拓撲概觀
copied-description: true
exl-id: ca5e8701-f8a3-4125-bb60-bfb9efd5c8f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---

# 網路拓撲概觀 {#network-topology-overview}

成功部署Adobe存取後，請務必維護環境安全性。 本節說明維護「Adobe存取」生產伺服器安全性所需的工作。

使用 *反向Proxy* 以確保外部和內部使用者都可使用Adobe存取Web應用程式的不同URL集。 此設定比允許使用者直接連線到執行Adobe存取的應用程式伺服器更安全。 反向Proxy會針對執行Adobe存取的應用程式伺服器執行所有HTTP要求。 使用者只有反向Proxy的網路存取權，而且只能嘗試反向Proxy支援的URL連線。

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)
