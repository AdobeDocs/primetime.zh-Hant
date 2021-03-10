---
title: 發行網域限制授權
description: 發行網域限制授權
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# 發佈網域限制授權{#issuing-domain-bound-licenses}

要使用需要域註冊的DRM策略發佈許可證，客戶機的請求必須包括由策略中指定的域伺服器發出的有效域令牌。 當用戶端要求授權時，會自動為任何網域伺服器加入網域Token，此網域Token是在內容中繼資料中指定的，但前提是用戶端已向這些網域伺服器註冊。 如果選取的DRM政策需要網域註冊，則SDK會自動從請求中選取網域Token，以將授權系結至，或傳回錯誤（如果找不到適當的網域Token）。

若網域Token未過期，且是由授權網域CA核發，則網域Token即視為有效。 授權伺服器必須指定網域授權，然後才能透過設定`HandlerConfiguration.setDomainCAs()`接受網域Token。 如果未配置域CA，則許可證伺服器將無法發放域綁定的許可證。

如果元資料包括多個DRM策略，則許可伺服器業務邏輯可以選擇基於客戶是否呈現域令牌的DRM策略。 您可以使用`LicenseRequestMessage.getDomainTokens()`來確定客戶機已註冊的域。
