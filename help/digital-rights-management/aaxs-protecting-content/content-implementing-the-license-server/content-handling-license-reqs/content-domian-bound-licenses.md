---
title: 發行網域繫結授權
description: 發行網域繫結授權
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 發行網域繫結授權{#issuing-domain-bound-licenses}

為了使用需要網域註冊的原則發行授權，使用者端的請求必須包含由原則中指定的網域伺服器發行的有效網域權杖。 當使用者端要求授權時，如果已經向內容中繼資料中指定的任何網域伺服器註冊，則會自動包含這些網域伺服器的網域權杖。 如果選取的原則需要網域註冊，SDK將會從要求中自動選取網域權杖以將授權繫結到，或者如果未找到適當的網域權杖，則會傳回錯誤。

如果網域權杖尚未過期，而且是由授權網域CA所簽發，則會視為有效。 授權伺服器必須透過設定來指定接受網域權杖的網域授權單位 `HandlerConfiguration.setDomainCAs()`. 如果未設定網域CA，授權伺服器將無法發行網域繫結的授權。

如果中繼資料包含多個原則，則授權伺服器商業邏輯會根據使用者端是否提供網域權杖來選取原則。 使用 `LicenseRequestMessage.getDomainTokens()` 以判斷使用者端註冊的網域。
