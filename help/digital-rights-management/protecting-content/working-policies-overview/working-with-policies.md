---
seo-title: 使用DRM策略概述
title: 使用DRM策略概述
uuid: 32423448-013c-4183-bea8-e14b6690abdb
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 概觀 {#working-with-drm-policies-overview}

內容提供者可使用Primetime DRM SDK，將DRM原則套用至媒體檔案。 然後，管理員可以使用原則管理API來建立、檢視DRM原則的詳細資訊並更新DRM原則。

A *`DRM policy`* 是資訊的集合，其中包含安全性設定、驗證要求和使用權限。 此原則定義使用者檢視內容的方式。 DRM政策、加密和簽署可讓內容提供者在內容散布多廣的情況下，仍能維持對其內容的控制。

DRM策略用作許可證伺服器在生成許可證時使用的模板。 客戶機也可以在請求許可之前參考DRM策略，以確定客戶機是否需要在向伺服器發出許可請求之前提示用戶進行驗證。

您可以使用Adobe Flash Media Server或HTTP伺服器來提供受保護的內容。 使用者可在使用Primetime DRM SDK建立的自訂播放器中下載及播放受保護的內容。

DRM策略指定授予客戶機的一個或多個權限。 通常，DRM策略至少包括 *`Play Right`*。 您也可以指定多個「播放權限」，每個「播放權限」具有不同的限制。 當用戶端收到具有多重播放權限的授權時，會使用第一個符合所有限制的授權。 例如，您可以在不同平台上強制執行不同的輸出保護設定。

有關 `CreatePolicyWithOutputProtection.java` 此示例的示例代碼，請參 [!DNL samples] 閱參考實施命令行工具目錄。

您可以使用Primetime DRM政策管理API完成下列工作：

* 建立和更新原則
* 查看DRM策略詳細資訊
* 管理DRM策略更新清單

如需Java *API的詳細資訊* ，請參閱Primetime DRM API參考。

如需Primetime DRM *政策管理員的相關資訊* ，請參閱使用Primetime DRM參考實作指南。
