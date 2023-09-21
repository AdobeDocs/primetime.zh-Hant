---
description: 若是熟悉Adobe Primetime Access DRM解決方案的人，Access與採用ExpressPlay解決方案的Primetime Cloud DRM之間在架構上有一些根本差異。
title: 從存取移轉至多個DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# 從存取移轉至多個DRM {#migrating-from-access-to-multi-drm}

若是熟悉Adobe Primetime Access DRM解決方案的人，Access與採用ExpressPlay解決方案的Primetime Cloud DRM之間在架構上有一些根本差異。

## 存取與多DRM之間的架構差異

|  | 存取 | 多DRM |
|---|---|---|
| **封裝** | Packager已繫結至授權伺服器。 封裝內容時，封裝程式必須知道授權伺服器的公開金鑰。 | 封裝程式未繫結至一個授權伺服器。 |
|  | 內容封裝後，就會繫結至特定的授權伺服器。 | 內容未繫結至特定的授權伺服器。 其效果之一是，您可以在取得生產授權之前封裝所有內容。 |
|  | Packager不需要與任何形式的金鑰儲存裝置通訊，因為金鑰在加密後會安全地嵌入到內容本身（在中繼資料中）中。 只有對應的授權伺服器可以讀取它們。 | 必須傳送金鑰 *至* 來自金鑰儲存系統的封裝者，或已傳送 *從* 封裝程式至金鑰儲存系統。 金鑰儲存系統可以是客戶自己的系統，也可以是ExpressPlay的金鑰儲存系統。 |
| **權利** | 使用者端向Access Cloud Service提出內容請求。 接著Access Cloud Service會向客戶的權益系統提出要求。 客戶的權益系統回應客戶的權益。 （使用者端在提出授權要求之前，可能已經從客戶伺服器取得登入的Cookie。） | 使用者端從客戶的店面要求權杖（這很可能與客戶先前取得驗證Cookie的相同工作流程）。 此時，客戶會執行權益檢查。 如果權益檢查通過，客戶會傳送要求給ExpressPlay伺服器，以便為客戶產生權杖。 此代號一律繫結至特定內容片段，且 *五月* 繫結至特定裝置。 客戶的店面會將Token傳回使用者端。 當使用者端發出DRM播放要求時，要求中會包含權杖（此方法僅適用於裝置），而ExpressPlay的DRM伺服器會驗證權杖，不會呼叫客戶的伺服器。 |
