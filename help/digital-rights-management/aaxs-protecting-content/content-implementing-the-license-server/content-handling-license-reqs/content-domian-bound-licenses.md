---
title: 頒發域綁定許可證
description: 頒發域綁定許可證
copied-description: true
exl-id: b9823ae4-d88f-4580-a2ce-275ed3e32f51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 頒發域綁定許可證{#issuing-domain-bound-licenses}

為了使用需要域註冊的策略頒發許可證，客戶端的請求必須包括由策略中指定的域伺服器頒發的有效域令牌。 當客戶端請求許可證時，如果已向這些域伺服器註冊，它將自動包括其內容元資料中指定的任何域伺服器的域令牌。 如果所選策略需要域註冊，SDK將自動從請求中選擇一個域令牌以將許可證綁定到，或在找不到適當的域令牌時返回錯誤。

如果域令牌未過期，並且是由授權域CA頒發的，則域令牌被視為有效。 許可證伺服器必須通過配置指定將接受域令牌的域授權 `HandlerConfiguration.setDomainCAs()`。 如果未配置域CA，則許可證伺服器將無法頒發域綁定的許可證。

如果元資料包括多個策略，則許可證伺服器業務邏輯可以基於客戶端是否呈現了域令牌來選擇策略。 使用 `LicenseRequestMessage.getDomainTokens()` 確定客戶機已註冊的域。
