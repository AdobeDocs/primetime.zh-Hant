---
title: 使用DRM策略概述
description: 使用DRM策略概述
copied-description: true
exl-id: 734d0be3-2abe-400c-bc34-00046ec52f4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 概述 {#working-with-drm-policies-overview}

內容提供者可以使用黃金時段DRM SDK將DRM策略應用到媒體檔案。 然後，管理員可以使用策略管理API建立、查看DRM策略的詳細資訊和更新DRM策略。

A *`DRM policy`* 是包含安全設定、身份驗證要求和使用權限的資訊的集合。 該策略定義用戶如何查看內容。 DRM策略、加密和簽名允許內容提供商保持對其內容的控制，而不管內容的分發範圍有多廣。

DRM策略用作許可證伺服器在生成許可證時使用的模板。 客戶機還可以在請求許可之前參考DRM策略，以確定客戶機是否需要在向伺服器發出許可請求之前提示用戶進行驗證。

您可以使用AdobeFlash Media Server或HTTP伺服器來傳遞受保護的內容。 用戶可以在使用黃金時段DRM SDK構建的定製播放器中下載和播放受保護的內容。

DRM策略指定授予客戶端的一個或多個權限。 通常，DRM策略至少包括 *`Play Right`*。 您還可以指定多個「播放權限」，每個權限具有不同的限制。 當客戶端收到具有多個播放權限的許可證時，它使用第一個滿足所有限制的許可證。 例如，可以在不同的平台上強制實施不同的輸出保護設定。

請參閱 `CreatePolicyWithOutputProtection.java` 在「參考實現」命令行工具中 [!DNL samples] 示例代碼的目錄。

您可以使用Mogfire DRM策略管理API完成以下任務：

* 建立和更新策略
* 查看DRM策略詳細資訊
* 管理DRM策略更新清單

查看 *黃金時段DRM API參考* 的子菜單。

查看 *使用黃金時段DRM參考實現* 指南。
