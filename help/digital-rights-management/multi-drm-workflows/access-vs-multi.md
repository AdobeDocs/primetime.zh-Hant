---
description: 對於熟悉AdobePrimetime Access DRM解決方案的人，Access和Primetime Cloud DRM（採用ExpressPlay解決方案）之間有一些基本的架構差異。
title: 從存取移轉至多DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# 從訪問遷移到多DRM {#migrating-from-access-to-multi-drm}

對於熟悉AdobePrimetime Access DRM解決方案的人，Access和Primetime Cloud DRM（採用ExpressPlay解決方案）之間有一些基本的架構差異。

## Access與多DRM的體系結構差異

|  | 存取 | 多DRM |
|---|---|---|
| **包裝** | Packager會系結至授權伺服器。 在封裝內容時，Packager必須知道授權伺服器的公開金鑰。 | Packager不綁定到一個許可證伺服器。 |
|  | 內容封裝後，即會系結至特定授權伺服器。 | 內容不會系結至特定的授權伺服器。 其中一個效果是，您可以在取得生產授權之前，先封裝所有內容。 |
|  | Packager不需要與任何形式的金鑰儲存體通訊，因為金鑰在加密後會安全地嵌入內容本身（在中繼資料中）。 只有對應的授權伺服器才能讀取。 | 密鑰必須從密鑰儲存系統發送&#x200B;*到*&#x200B;包裝器，或從&#x200B;*包裝器發送*&#x200B;到密鑰儲存系統。 密鑰儲存系統可以是客戶自己的系統，也可以是ExpressPlay的密鑰儲存。 |
| **權益** | 用戶端會向Access Cloud服務要求內容。 接著，Access雲端服務會向客戶的權益系統提出要求。 客戶的權益系統會以客戶的權益回覆。 （客戶在提出授權要求之前，可能已從客戶的伺服器取得Cookie以進行登入。） | 客戶從客戶店面要求代號（這可能與客戶先前收到驗證Cookie的工作流程相同）。 目前，客戶會執行權益檢查。 如果權益檢查通過，客戶會傳送請求至ExpressPlay伺服器，以產生客戶的代號。 此Token一律系結至特定內容，而&#x200B;*可*&#x200B;系結至特定裝置。 客戶的店面會將代號傳回給客戶。 當用戶端提出DRM播放要求時，代號會包含在要求中（這種方法是裝置特定的），而ExpressPlay的DRM伺服器會驗證代號，而不會呼叫客戶的伺服器。 |