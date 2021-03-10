---
title: 網路拓撲概述
description: 網路拓撲概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 網路拓撲概述{#network-topology-overview}

在成功部署Adobe訪問後，維護環境的安全至關重要。 本節介紹維護Adobe訪問生產伺服器安全所需的任務。

使用&#x200B;*reverse proxy*&#x200B;來確保外部和內部使用者都能使用Adobe存取Web應用程式的不同URL集。 此配置比允許用戶直接連接到運行Adobe訪問的應用程式伺服器更安全。 反向代理會對運行Adobe訪問的應用程式伺服器執行所有HTTP請求。 使用者只能透過網路存取反向代理，且只能嘗試反向代理支援的URL連線。

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

