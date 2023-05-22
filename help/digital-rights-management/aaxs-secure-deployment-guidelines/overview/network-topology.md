---
title: 網路拓撲概述
description: 網路拓撲概述
copied-description: true
exl-id: ca5e8701-f8a3-4125-bb60-bfb9efd5c8f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---

# 網路拓撲概述 {#network-topology-overview}

在成功部署Adobe訪問後，維護環境的安全性非常重要。 本節介紹維護Adobe訪問生產伺服器安全所需的任務。

使用 *反向代理* 確保外部和內部用戶都可以使用用於AdobeAccess Web應用程式的不同URL集。 此配置比允許用戶直接連接到運行Adobe訪問的應用程式伺服器更安全。 反向代理對運行Adobe訪問的應用程式伺服器執行所有HTTP請求。 用戶只有對反向代理的網路訪問權限，並且只能嘗試反向代理支援的URL連接。

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)
