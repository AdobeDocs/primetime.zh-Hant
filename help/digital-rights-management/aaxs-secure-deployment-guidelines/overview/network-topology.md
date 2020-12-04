---
seo-title: 網路拓撲概述
title: 網路拓撲概述
uuid: 1558b7fa-dc0d-477c-8f1c-9c6f3718e1b0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 網路拓撲概述{#network-topology-overview}

在您成功部署Adobe Access後，請務必維護您環境的安全性。 本節說明維護Adobe Access生產伺服器安全性所需的工作。

使用&#x200B;*反向proxy*&#x200B;來確保Adobe Access網頁應用程式的不同URL集可供外部和內部使用者使用。 此設定比讓使用者直接連線至執行Adobe Access的應用程式伺服器更安全。 反向代理會針對執行Adobe Access的應用程式伺服器執行所有HTTP請求。 使用者只能透過網路存取反向代理，且只能嘗試反向代理支援的URL連線。

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

