---
seo-title: Primetime DRM在用戶端上
title: Primetime DRM在用戶端上
uuid: 472180ad-6596-4a24-aa51-7909a75a5e10
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Primetime DRM在用戶端上{#primetime-drm-on-the-client}

播放受保護內容的Primetime TVSDK應用程式必須先呼叫Primetime DRM API，以啟動授權使用和受保護內容播放的工作流程。 在此工作流程中，用戶端上的Primetime DRM從受保護內容的中繼資料建構授權要求，然後將其傳送至Primetime DRM授權伺服器。

在發出授權要求之前，客戶可選擇執行必要的驗證／授權（視您的業務規則而定）。
