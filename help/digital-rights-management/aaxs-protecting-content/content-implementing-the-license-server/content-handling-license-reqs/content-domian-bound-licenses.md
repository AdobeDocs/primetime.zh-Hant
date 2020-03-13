---
seo-title: 發行限制網域的授權
title: 發行限制網域的授權
uuid: 175d3b7d-d1df-44ee-85ad-a0db4a1bdb9d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 發行限制網域的授權{#issuing-domain-bound-licenses}

為了使用需要域註冊的策略發放許可證，客戶機的請求必須包括策略中指定的域伺服器發出的有效域令牌。 當用戶端要求授權時，如果已向這些網域伺服器註冊，就會自動將其網域Token加入內容中繼資料中指定的網域伺服器。 如果選取的原則需要網域註冊，SDK會自動從請求中選取網域Token，以將授權系結至，或在找不到適當的網域Token時傳回錯誤。

若網域Token未過期，且是由授權網域CA核發，則網域Token即視為有效。 授權伺服器必須透過設定，指定接受網域Token的網域授權機構 `HandlerConfiguration.setDomainCAs()`。 如果未配置域CA，則許可證伺服器將無法發放域綁定的許可證。

如果元資料包括多個策略，則許可證伺服器業務邏輯可以根據客戶端是否呈現域令牌來選擇策略。 用 `LicenseRequestMessage.getDomainTokens()` 於確定客戶機已註冊的域。
