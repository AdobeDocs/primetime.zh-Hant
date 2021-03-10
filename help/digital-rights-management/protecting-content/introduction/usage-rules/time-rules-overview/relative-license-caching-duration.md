---
title: 授權快取持續時間
description: 授權快取持續時間
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 授權快取持續時間{#license-caching-duration}

授權快取持續時間可指定授權可快取至用戶端本機License Store磁碟上的時間長度，而不需從授權伺服器重新取得。 或者，您可以指定絕對日期和時間，之後將無法再快取授權。

快取到期日一經過，授權就不再有效，而且用戶端必須向授權伺服器要求新的授權。

範例使用案例：使用授權快取持續時間來指定特定授權的固定有效時間，例如租用使用案例。 您可以指定30天租金（含授權快取），以指出要使用內容的授權總持續時間。
