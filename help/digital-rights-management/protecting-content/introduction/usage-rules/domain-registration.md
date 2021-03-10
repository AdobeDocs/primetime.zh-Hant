---
title: 設備組域註冊
description: 設備組域註冊
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 設備組域註冊{#device-group-domain-registration}

Primetime DRM 3.0或更新版本支援將授權系結至裝置網域，做為將授權系結至特定裝置的替代選擇。

多個設備可以加入域並接收域Token。 在域中的設備獲得許可後，許可證可以被傳輸到域中的任何其他設備，這些設備可以播放內容而無需直接從許可證伺服器獲取許可證。

如果您想要支援任何網域系結的授權，則Primetime DRM政策必須指定用戶端必須註冊的網域伺服器。 Primetime DRM策略還必須指定域伺服器的驗證要求，無論是啟用匿名訪問還是伺服器需要用戶名／密碼還是自定義驗證。

Primetime DRM用戶端3.0版或更新版本支援網域註冊和網域系結授權。 如果Flash Player中較舊的客戶或Adobe Primetime3.0客戶端請求支援域註冊的內容的許可，則許可伺服器可能會發放使用替代Primetime DRM策略以支援綁定到特定設備的許可。
