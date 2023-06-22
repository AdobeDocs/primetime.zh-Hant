---
title: BEES概述
description: BEES概述
copied-description: true
exl-id: 481af72b-40a3-4f33-9e91-990dc5308596
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# BEES概述{#bees-overview}

您可以實作後端權益服務(BEES)，為您的Primetime Cloud DRM操作提供自訂權益。

Primetime Cloud DRM預設使用匿名授權傳遞。 這表示傳送至Primetime Cloud DRM的所有授權要求都將傳回有效的授權，而不執行任何其他驗證/授權檢查(除非您已套用原則限制，要求使用Adobe Primetime驗證)。

授權要求包含內容封裝/加密期間所使用的DRM原則。 DRM政策用於產生傳回給使用者端的DRM授權。 在預設情況下，您必須在內容封裝時做出所有DRM政策決定。 想要更精細地控制這些工作流程的客戶有以下選項：

1. 整合Primetime驗證，以在播放前新增額外的權益檢查。
1. 建立內部部署軟體權利服務，Primetime Cloud DRM在允許任何裝置播放您已封裝的內容之前會查詢此服務。

您的內部部署軟體權利檔案服務必須提供對Primetime Cloud DRM的回應，包括以下兩個資料片段：

* `isAllowed`
* `drmPolicyToUse`

這些選項決定裝置是否允許播放內容，以及使用哪個DRM原則來產生DRM授權(如果 `isAllowed` 為true)。

本檔案說明完成上述選項2所需執行的操作：實作您自己的內部部署外部權利服務，並使其可供Primetime Cloud DRM使用您已封裝的內容。
