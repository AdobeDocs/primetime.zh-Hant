---
seo-title: 設備組域註冊
title: 設備組域註冊
uuid: fd559175-2c3c-4d71-bfa1-8de9907d2b7c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 設備組域註冊{#device-group-domain-registration}

除了將授權系結至特定裝置以外，Adobe Access 3.0和更新版本支援將授權系結至裝置網域。 多個設備可以加入域並接收域Token。 在域中的設備獲得許可後，許可證可以被傳輸到域中的任何其他設備，這些設備可以播放內容而無需直接從許可證伺服器獲取許可證。

要支援域綁定許可證，策略必須指定客戶端必須註冊的域伺服器。 策略還將指定域伺服器的驗證要求（是否允許匿名訪問，或伺服器是否需要用戶名／密碼或自定義驗證）。

Adobe Access用戶端3.0版及更新版本支援網域註冊和網域系結授權。 如果舊版用戶端或Flash Player中的Adobe Access 3.0用戶端要求取得支援網域註冊的內容授權，授權伺服器可能會使用支援系結至特定裝置的替代政策來核發授權。
