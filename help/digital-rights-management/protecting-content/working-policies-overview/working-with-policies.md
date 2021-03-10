---
title: 使用DRM策略概述
description: 使用DRM策略概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 概述{#working-with-drm-policies-overview}

內容提供者可使用Primetime DRM SDK，將DRM原則套用至媒體檔案。 然後，管理員可以使用原則管理API來建立、檢視DRM原則的詳細資訊，並更新DRM原則。

*`DRM policy`*&#x200B;是包含安全性設定、驗證要求和使用權限的資訊集合。 此原則定義使用者檢視內容的方式。 DRM政策、加密和簽署可讓內容提供者在內容散布多廣的情況下，仍能維持對其內容的控制。

DRM策略用作許可證伺服器在生成許可證時使用的模板。 客戶機也可以在請求許可之前參考DRM策略，以確定客戶機是否需要在向伺服器發出許可請求之前提示用戶進行驗證。

您可以使用AdobeFlash Media Server或HTTP伺服器來傳送受保護的內容。 使用者可在使用Primetime DRM SDK建立的自訂播放器中下載及播放受保護的內容。

DRM策略指定授予客戶機的一個或多個權限。 通常，DRM策略至少包括&#x200B;*`Play Right`*。 您也可以指定多個「播放權限」，每個「播放權限」具有不同的限制。 當用戶端收到具有多重播放權限的授權時，會使用第一個符合所有限制的授權。 例如，您可以在不同平台上強制執行不同的輸出保護設定。

有關說明此示例的示例代碼，請參見Reference Implementation Command Line Tools [!DNL samples]目錄中的`CreatePolicyWithOutputProtection.java`。

您可以使用Primetime DRM政策管理API完成下列工作：

* 建立和更新原則
* 查看DRM策略詳細資訊
* 管理DRM策略更新清單

如需Java API的詳細資訊，請參閱&#x200B;*Primetime DRM API參考*。

有關Primetime DRM策略管理器的資訊，請參閱&#x200B;*使用Primetime DRM參考實施*&#x200B;指南。
