---
description: 適用於受保護串流的Adobe Primetime DRM伺服器是以Primetime DRM SDK為基礎的授權伺服器實作。 此伺服器會向Primetime DRM使用者端發行受保護內容的授權。
title: 關於用於受保護串流的Adobe Primetime DRM伺服器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 關於用於受保護串流的Adobe Primetime DRM伺服器{#about-adobe-primetime-drm-server-for-protected-streaming}

適用於受保護串流的Adobe Primetime DRM伺服器是以Primetime DRM SDK為基礎的授權伺服器實作。 此伺服器會向Primetime DRM使用者端發行受保護內容的授權。

Primetime DRM Server for Protected Streaming支援多個租使用者。 您可以代表多個內容發佈者託管單一伺服器，每個發佈者都有自己的組態設定。 此外，伺服器支援自訂授權元件，因此您可以在核發授權之前執行自訂邏輯。

此伺服器旨在搭配HTTP資料流使用。 因此，此伺服器實作不支援Primetime DRM中可用的所有功能。 例如，它不支援使用者驗證請求、多個原則、網域繫結授權、授權鏈結或同步處理訊息。

>[!NOTE]
>
>Adobe Primetime DRM先前稱為Adobe存取，在此之前則為Flash Access。
