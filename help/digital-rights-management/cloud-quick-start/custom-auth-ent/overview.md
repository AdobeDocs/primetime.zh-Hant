---
title: 蜂類概述
description: 蜂類概述
copied-description: true
exl-id: 481af72b-40a3-4f33-9e91-990dc5308596
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 蜂類概述{#bees-overview}

您可以實施後端權利服務(BEES)，為您的黃金時段雲DRM操作提供自定義權利。

預設情況下，Mighine Cloud DRM使用匿名許可證交付。 這意味著發送到Mighile Cloud DRM的所有許可證請求將返回有效的許可證，而無需執行任何附加的驗證/授權檢查(除非您應用了需要使用Adobe Primetime驗證的策略約束)。

許可請求包含在內容打包/加密期間使用的DRM策略。 DRM策略用於生成返回給客戶機的DRM許可。 在預設情況下，必須在內容打包時做出所有DRM策略決定。 希望對這些工作流進行更精確控制的客戶具有以下選項：

1. 整合Mogifale身份驗證以在播放前添加額外權利檢查。
1. 建立Mogifale Cloud DRM將在允許任何設備播放您打包的內容之前查詢的本地權利服務。

您的本地權利服務必須提供對黃金時段雲DRM的響應，該響應包括以下兩條資料：

* `isAllowed`
* `drmPolicyToUse`

這些確定是否允許設備播放內容，以及使用哪個DRM策略來生成DRM許可(如果 `isAllowed` 為真)。

本文檔介紹了完成上述選項2所需做的工作：實施您自己的內部外部權利服務，並使其可用於Mighaile Cloud DRM，以獲取您打包的內容。
