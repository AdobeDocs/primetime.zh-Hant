---
title: 增強的授權鏈結
description: 增強的授權鏈結
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 增強的授權鏈結{#enhanced-license-chaining}

您可以使用增強的授權鏈結，使用父根授權來批次更新授權，以更新授權。

Primetime DRM 2.0支援授權鏈結，其中葉片授權和根授權皆系結至特定機器。 Primetime DRM 3.0和更新版本支援增強的授權鏈結，其中葉片系結至根授權，而只有根授權系結至特定機器或網域。 增強的授權鏈結支援將葉片授權內嵌在內容中，而用戶端只需從授權伺服器取得根授權，即可使用受保護的內容。

如果您想要啟用增強的授權鏈結，則必須將根加密金鑰指派給Primetime DRM政策。 根加密密鑰用於以密碼方式將葉許可證綁定到根許可證。

>[!NOTE]
>
>Primetime DRM用戶端3.0版或更新版本支援增強的授權鏈結。 如果舊版用戶端要求支援增強授權鏈結的內容授權，授權伺服器仍可使用Primetime DRM 2.0支援的授權鏈結，向此用戶端發放授權。

範例使用案例：使用這個選項，下載單一根授權以更新任何連結的授權。 例如，實作訂閱模型，只要使用者每月重新訂閱，就可播放內容。 此方法的優點在於，使用者只需取得單一授權，即可更新其所有訂閱授權。
