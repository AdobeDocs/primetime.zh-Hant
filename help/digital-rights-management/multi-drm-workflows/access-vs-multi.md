---
description: 若是熟悉AdobePrimetime Access DRM解決方案的人，Access與採用ExpressPlay解決方案的Primetime Cloud DRM在架構上有一些根本差異。
title: 從存取移轉至多個DRM
exl-id: f5e4cd88-091d-4049-933d-1c72ceeb2efb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# 從存取移轉至多個DRM {#migrating-from-access-to-multi-drm}

若是熟悉AdobePrimetime Access DRM解決方案的人，Access與採用ExpressPlay解決方案的Primetime Cloud DRM在架構上有一些根本差異。

## 存取與多DRM之間的架構差異

|  | 存取 | 多DRM |
|---|---|---|
| **封裝** | Packager已繫結至授權伺服器。 封裝內容時，封裝程式必須知道授權伺服器的公開金鑰。 | Packager未繫結至一個授權伺服器。 |
|  | 內容封裝後，就會繫結至特定的授權伺服器。 | 內容未繫結至特定的授權伺服器。 其中一種效果是，您可以在取得生產授權之前封裝所有內容。 |
|  | Packager不需要與任何形式的金鑰儲存裝置通訊，因為金鑰在加密後會安全地嵌入到內容本身（在中繼資料中）中。 只有對應的授權伺服器可以讀取它們。 | 必須傳送金鑰 *至* 來自金鑰儲存系統的封包程式，或已傳送 *從* 金鑰儲存系統的封裝程式。 金鑰儲存系統可以是客戶自己的系統，也可以是ExpressPlay的金鑰儲存系統。 |
| **權利** | 使用者端向Access Cloud Service提出內容請求。 接著Access Cloud Service會向客戶的權益系統提出要求。 客戶的權益系統回應提供客戶的權益。 （使用者端提出授權要求之前，可能已經從客戶伺服器取得登入的Cookie。） | 使用者端從客戶的店面要求Token （這很可能與客戶先前取得驗證Cookie的工作流程相同）。 此時，客戶會執行權益檢查。 如果權益檢查通過，客戶會傳送請求給ExpressPlay伺服器，以便為客戶產生Token。 此Token一律繫結至特定內容片段，並且 *五月* 繫結至特定裝置。 客戶的店面會將Token傳送回使用者端。 當使用者端提出DRM播放請求時，該權杖會包含在請求中（此方法適用於特定裝置），而且ExpressPlay的DRM伺服器會驗證該權杖，而不會呼叫客戶的伺服器。 |
