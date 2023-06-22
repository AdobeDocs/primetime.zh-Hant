---
title: 發行網域繫結的授權
description: 發行網域繫結的授權
copied-description: true
exl-id: c29e61e5-d05a-4744-9ec8-7508ed814a57
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 發行網域繫結的授權{#issuing-domain-bound-licenses}

若要使用需要網域註冊的DRM原則發行授權，使用者端的請求必須包含原則中指定的網域伺服器所發行的有效網域權杖。 當使用者端要求授權時，會自動包含其網域權杖，用於內容中繼資料中指定的任何網域伺服器，前提是它已向這些網域伺服器註冊。 如果選取的DRM原則需要網域註冊，則SDK接著會從要求中自動選取網域權杖以將授權繫結到，或如果找不到適當的網域權杖，則會傳回錯誤。

如果網域權杖尚未過期，而且是由授權網域CA發行，則視為有效。 授權伺服器必須指定網域授權單位，然後透過設定來接受網域權杖 `HandlerConfiguration.setDomainCAs()`. 如果未設定網域CA，授權伺服器將無法發行網域繫結的授權。

如果中繼資料包含多個DRM原則，則授權伺服器商業邏輯可以根據使用者端是否提供網域權杖來選取DRM原則。 您可以使用 `LicenseRequestMessage.getDomainTokens()` 以判斷使用者端已註冊的網域。
