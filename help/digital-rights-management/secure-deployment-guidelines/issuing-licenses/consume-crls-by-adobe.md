---
description: SDK會定期下載由Adobe發佈的CRL。 您必須確保不會封鎖對這些檔案的存取，或不會妨礙這些CRL的執行。
seo-description: SDK會定期下載由Adobe發佈的CRL。 您必須確保不會封鎖對這些檔案的存取，或不會妨礙這些CRL的執行。
seo-title: 使用Adobe發佈的CRL
title: 使用Adobe發佈的CRL
uuid: 7a9088bd-dde6-4445-958c-3e7272215b3c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用Adobe發佈的CRL{#consuming-crls-published-by-adobe}

SDK會定期下載由Adobe發佈的CRL。 您必須確保不會封鎖對這些檔案的存取，或不會妨礙這些CRL的執行。

SDK有設定選項，可在擷取Adobe CRL時忽略錯誤，而您只能在開發環境中套用此選項。 在生產環境中，授權伺服器必須從Adobe擷取CRL。 如果授權伺服器無法取得有效的CRL，就會發生錯誤。
