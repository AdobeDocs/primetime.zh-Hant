---
title: 設備組域註冊
description: 設備組域註冊
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 設備組域註冊{#device-group-domain-registration}

除了將授權系結至特定裝置以外，AdobeAccess 3.0和更新版本支援將授權系結至裝置網域。 多個設備可以加入域並接收域Token。 在域中的設備獲得許可後，許可證可以被傳輸到域中的任何其他設備，這些設備可以播放內容而無需直接從許可證伺服器獲取許可證。

要支援域綁定許可證，策略必須指定客戶端必須註冊的域伺服器。 策略還將指定域伺服器的驗證要求（是否允許匿名訪問，或伺服器是否需要用戶名／密碼或自定義驗證）。

Adobe存取用戶端3.0版及更新版本支援網域註冊和網域系結授權。 如果Flash Player中較舊的客戶機或AdobeAccess 3.0客戶機請求支援域註冊的內容的許可證，則許可證伺服器可能會使用支援綁定到特定設備的替代策略頒發許可證。
