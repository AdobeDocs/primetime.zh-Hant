---
title: 發行網域繫結授權
description: 發行網域繫結授權
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 發行網域繫結授權{#issuing-domain-bound-licenses}

若要使用需要網域註冊的DRM原則發行授權，使用者端的請求必須包含由原則中指定的網域伺服器發行的有效網域權杖。 當使用者端要求授權時，它會自動納入其網域伺服器的網域權杖，該網域伺服器會在使用者端已註冊這些網域伺服器的內容中繼資料中指定。 如果選取的DRM原則需要網域註冊，則SDK接著會從要求中自動選取網域權杖以將授權繫結到，如果未找到適當的網域權杖，則會傳回錯誤。

如果網域權杖尚未過期，而且是由授權網域CA所簽發，則會視為有效。 授權伺服器必須指定網域授權單位，然後透過設定來接受網域權杖 `HandlerConfiguration.setDomainCAs()`. 如果未設定網域CA，授權伺服器將無法發行網域繫結的授權。

如果中繼資料包含多個DRM原則，則授權伺服器商業邏輯可依據使用者端是否提供網域權杖來選取DRM原則。 您可以使用 `LicenseRequestMessage.getDomainTokens()` 以判斷使用者端註冊的網域。
