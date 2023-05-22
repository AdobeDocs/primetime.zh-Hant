---
title: 關於Adobe Access Server的受保護流
description: 關於Adobe Access Server的受保護流
copied-description: true
exl-id: 69fbc99d-ee1a-4066-ae01-d61838db32a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 關於Adobe Access Server的受保護流{#about-adobe-access-server-for-protected-streaming}

Adobe® Access™ Server for Protected Streaming是基於Adobe訪問SDK的許可證伺服器實現。 此伺服器向Adobe訪問客戶端頒發受保護內容的許可證。

「受保護流」的Adobe Access Server支援多個租戶，這意味著可以代表多個內容發佈者托管單個伺服器，每個發佈者都具有自己的配置設定。 此外，伺服器支援自定義授權元件，因此可以在頒發許可證之前執行自定義邏輯。

此伺服器用於HTTP流。 因此，此伺服器實現不支援Adobe訪問中可用的所有功能。 例如，受保護流的Adobe Access Server不支援用戶身份驗證請求、多個策略、域綁定的許可證、許可證連結或同步消息。
