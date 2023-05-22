---
description: 用於受保護流的Adobe PrimetimeDRM伺服器是基於黃金時段DRM SDK的許可證伺服器實現。 此伺服器向黃金時段DRM客戶端發放受保護內容的許可證。
title: 關於Adobe PrimetimeDRM伺服器，用於受保護的流
exl-id: 911acd61-8b27-4ac7-a420-2faeb46e8087
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 關於Adobe PrimetimeDRM伺服器，用於受保護的流{#about-adobe-primetime-drm-server-for-protected-streaming}

用於受保護流的Adobe PrimetimeDRM伺服器是基於黃金時段DRM SDK的許可證伺服器實現。 此伺服器向黃金時段DRM客戶端發放受保護內容的許可證。

用於受保護流的黃金時段DRM伺服器支援多個租戶。 您可以代表多個內容發佈者來托管單個伺服器，每個伺服器都具有自己的配置設定。 此外，伺服器支援自定義授權元件，因此您可以在頒發許可證之前執行自定義邏輯。

此伺服器用於HTTP流。 因此，此伺服器實現不支援黃金時段DRM中可用的所有功能。 例如，它不支援用戶身份驗證請求、多個策略、域綁定的許可證、許可證連結或同步消息。

>[!NOTE]
>
>Adobe PrimetimeDRM以前叫做Adobe訪問，在之前叫Flash Access。
