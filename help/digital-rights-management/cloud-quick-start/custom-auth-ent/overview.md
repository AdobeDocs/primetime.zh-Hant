---
seo-title: 蜜蜂概觀
title: 蜜蜂概觀
uuid: c6ee7528-fdfa-4a56-bea2-a5e2dab6d428
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 蜜蜂概觀{#bees-overview}

您可以實作後端權益服務(BEES)，為您的Primetime Cloud DRM作業提供自訂權益。

Primetime Cloud DRM預設會使用匿名授權傳送。 這表示所有傳送至Primetime Cloud DRM的授權要求都會傳回有效的授權，而不需執行任何額外的驗證／授權檢查（除非您套用了需要使用Adobe Primetime驗證的原則限制）。

授權要求包含在內容封裝／加密期間採用的DRM原則。 DRM策略用於生成返回給客戶機的DRM許可。 在預設情況下，您必須在內容封裝時做出所有DRM政策決策。 想要對這些工作流程進行更精細控制的客戶有下列選項：

1. 整合Primetime驗證，在播放前新增額外權益檢查。
1. 建立Primetime Cloud DRM在允許任何裝置播放已封裝內容之前，將會先查詢的內部權益服務。

您的內部權益服務必須提供對Primetime Cloud DRM的回應，其中包含下列兩項資料：

* `isAllowed`
* `drmPolicyToUse`

這些決定是否允許裝置播放內容，以及用來產生DRM授權的DRM政策(如果 `isAllowed` 為真)。

本檔案涵蓋您完成上述選項2所需要執行的工作：實作您自己的內部外部權益服務，並將它提供給Primetime Cloud DRM，以取得您已封裝的內容。
