---
title: 設備組域註冊
description: 設備組域註冊
copied-description: true
exl-id: 1f3e9d26-c185-4d12-accf-aa74a313f890
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 設備組域註冊{#device-group-domain-registration}

作為將許可證綁定到特定設備的替代方法，AdobeAccess 3.0及更高版本支援將許可證綁定到設備域。 多個設備可以加入域並接收域令牌。 在域中的設備獲取許可證之後，許可證可以被傳輸到域中的任何其他設備，並且這些設備可以播放內容而無需直接從許可證伺服器獲取許可證。

要支援域綁定的許可證，策略必須指定客戶端必須註冊的域伺服器。 策略還將指定域伺服器的身份驗證要求（是否允許匿名訪問或伺服器是否需要用戶名/密碼或自定義身份驗證）。

Adobe訪問客戶端3.0及更高版本支援域註冊和域綁定許可證。 如果Flash Player中的較舊客戶端或AdobeAccess 3.0客戶端請求支援域註冊的內容的許可證，則許可證伺服器可以使用支援綁定到特定設備的替代策略來頒發許可證。
