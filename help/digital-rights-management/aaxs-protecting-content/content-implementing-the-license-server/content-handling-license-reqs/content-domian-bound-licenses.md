---
title: 發行網域繫結的授權
description: 發行網域繫結的授權
copied-description: true
exl-id: b9823ae4-d88f-4580-a2ce-275ed3e32f51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 發行網域繫結的授權{#issuing-domain-bound-licenses}

若要使用需要網域註冊的原則發行授權，使用者端的請求必須包含由原則中指定的網域伺服器發行的有效網域權杖。 當使用者端要求授權時，如果已向內容中繼資料中指定的任何網域伺服器註冊，則會自動包含這些網域伺服器的網域權杖。 如果選取的原則需要網域註冊，SDK將會從要求中自動選取網域權杖以將授權繫結到，或在找不到適當的網域權杖時傳回錯誤。

如果網域權杖尚未過期，而且是由授權網域CA發行，則視為有效。 授權伺服器必須透過設定來指定接受網域權杖的網域授權單位 `HandlerConfiguration.setDomainCAs()`. 如果未設定網域CA，授權伺服器將無法發行網域繫結的授權。

如果中繼資料包含多個原則，則授權伺服器商業邏輯可以根據使用者端是否提供網域權杖來選取原則。 使用 `LicenseRequestMessage.getDomainTokens()` 以判斷使用者端已註冊的網域。
