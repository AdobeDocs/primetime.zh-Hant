---
description: 適用於受保護串流的Adobe Primetime DRM伺服器是以Primetime DRM SDK為基礎的授權伺服器實作。 此伺服器會向Primetime DRM使用者端發行受保護內容的授權。
title: 關於受保護串流的Adobe Primetime DRM伺服器
exl-id: 911acd61-8b27-4ac7-a420-2faeb46e8087
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 關於受保護串流的Adobe Primetime DRM伺服器{#about-adobe-primetime-drm-server-for-protected-streaming}

適用於受保護串流的Adobe Primetime DRM伺服器是以Primetime DRM SDK為基礎的授權伺服器實作。 此伺服器會向Primetime DRM使用者端發行受保護內容的授權。

Primetime DRM Server for Protected Streaming支援多個租使用者。 您可以代表多個內容發行者託管單一伺服器，每個發行者都有自己的組態設定。 此外，伺服器支援自訂授權元件，因此您可以在核發授權之前執行自訂邏輯。

此伺服器旨在搭配HTTP串流使用。 因此，此伺服器實作不支援Primetime DRM中可用的所有功能。 例如，它不支援使用者驗證請求、多個原則、網域繫結授權、授權鏈結或同步化訊息。

>[!NOTE]
>
>Adobe Primetime DRM先前稱為Adobe存取，之前稱為Flash Access。
