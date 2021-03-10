---
title: 發行限制網域的授權
description: 發行限制網域的授權
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 發行網域系結授權{#issuing-domain-bound-licenses}

為了使用需要域註冊的策略發放許可證，客戶機的請求必須包括策略中指定的域伺服器發出的有效域令牌。 當用戶端要求授權時，如果已向這些網域伺服器註冊，就會自動將其網域Token加入內容中繼資料中指定的網域伺服器。 如果選取的原則需要網域註冊，SDK會自動從請求中選取網域Token，以將授權系結至，或在找不到適當的網域Token時傳回錯誤。

若網域Token未過期，且是由授權網域CA核發，則網域Token即視為有效。 授權伺服器必須透過設定`HandlerConfiguration.setDomainCAs()`，指定接受網域Token的網域授權。 如果未配置域CA，則許可證伺服器將無法發放域綁定的許可證。

如果元資料包括多個策略，則許可證伺服器業務邏輯可以根據客戶端是否呈現域令牌來選擇策略。 使用`LicenseRequestMessage.getDomainTokens()`確定客戶端已註冊的域。
