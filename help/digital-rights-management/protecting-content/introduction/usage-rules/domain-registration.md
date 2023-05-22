---
title: 設備組域註冊
description: 設備組域註冊
copied-description: true
exl-id: 81d6023b-76e0-4786-805b-bfe77e9f8513
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# 設備組域註冊{#device-group-domain-registration}

作為將許可證綁定到特定設備的替代方法，黃金時段DRM 3.0或更高版本支援將許可證綁定到設備域。

多個設備可以加入域並接收域令牌。 在域中的設備獲取許可證之後，許可證可以被傳輸到域中的任何其他設備，並且這些設備可以播放內容而無需直接從許可證伺服器獲取許可證。

如果要支援任何域綁定的許可證，則黃金時段DRM策略必須指定客戶端必須向其註冊的域伺服器。 黃金時段DRM策略還必須指定域伺服器的驗證要求，無論是啟用匿名訪問還是伺服器需要用戶名/密碼還是自定義驗證。

Mogine DRM客戶端3.0版或更高版本支援域註冊和域綁定許可證。 如果Flash Player中的較舊客戶機或Adobe Primetime3.0客戶機請求支援域註冊的內容的許可證，則許可證伺服器可以發出使用替代的黃金時段DRM策略支援綁定到特定設備的許可證。
