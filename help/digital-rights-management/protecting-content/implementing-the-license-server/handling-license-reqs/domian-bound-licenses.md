---
title: 頒發域綁定許可證
description: 頒發域綁定許可證
copied-description: true
exl-id: c29e61e5-d05a-4744-9ec8-7508ed814a57
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 頒發域綁定許可證{#issuing-domain-bound-licenses}

要使用需要域註冊的DRM策略發佈許可證，客戶端的請求必須包括由策略中指定的域伺服器發出的有效域令牌。 當客戶端請求許可證時，它自動為內容元資料中指定的任何域伺服器包括其域令牌，前提是它已向這些域伺服器註冊。 如果所選的DRM策略需要域註冊，則SDK隨後從請求中自動選擇域令牌以將許可證綁定到，或者如果找不到適當的域令牌，則返回錯誤。

如果域令牌未過期，並且是由授權域CA頒發的，則域令牌被視為有效。 許可證伺服器必須指定域授權，然後通過配置來接受域令牌 `HandlerConfiguration.setDomainCAs()`。 如果未配置域CA，則許可證伺服器將無法頒發域綁定的許可證。

如果元資料包括多個DRM策略，則許可證伺服器業務邏輯可以基於客戶端是否呈現域令牌來選擇DRM策略。 您可以使用 `LicenseRequestMessage.getDomainTokens()` 確定客戶機已註冊的域。
