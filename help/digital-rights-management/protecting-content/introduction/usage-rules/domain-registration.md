---
seo-title: 設備組域註冊
title: 設備組域註冊
uuid: 221bf6c3-0568-443d-b761-64715a57ada6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 設備組域註冊{#device-group-domain-registration}

Primetime DRM 3.0或更新版本支援將授權系結至裝置網域，做為將授權系結至特定裝置的替代選擇。

多個設備可以加入域並接收域Token。 在域中的設備獲得許可後，許可證可以被傳輸到域中的任何其他設備，這些設備可以播放內容而無需直接從許可證伺服器獲取許可證。

如果您想要支援任何網域系結的授權，則Primetime DRM政策必須指定用戶端必須註冊的網域伺服器。 Primetime DRM策略還必須指定域伺服器的驗證要求，無論是啟用匿名訪問還是伺服器需要用戶名／密碼還是自定義驗證。

Primetime DRM用戶端3.0版或更新版本支援網域註冊和網域系結授權。 如果舊版用戶端或Flash Player中的Adobe Primetime 3.0用戶端要求取得支援網域註冊的內容授權，授權伺服器可能會核發使用替代Primetime DRM政策以支援系結至特定裝置的授權。
