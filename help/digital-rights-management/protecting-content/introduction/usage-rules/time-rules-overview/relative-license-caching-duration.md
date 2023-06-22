---
title: 授權快取持續時間
description: 授權快取持續時間
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 授權快取持續時間{#license-caching-duration}

授權快取持續時間會指定在使用者端的本機授權存放區中，授權可以在磁碟上快取多久的時間，而不需要從授權伺服器重新贏取。 或者，您可以指定絕對日期和時間，之後再也無法快取授權。

快取到期日過後，授權就不再有效，使用者端必須向授權伺服器要求新的授權。

使用案例範例：使用授權快取持續時間來指定特定授權的有效固定時間量，例如在租賃使用案例中。 您可以指定30天租用（含授權快取），以指出使用內容的總授權期間。
