---
title: DRM策略關鍵性
description: DRM策略關鍵性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# DRM策略重要性{#drm-policy-criticality}

如果您打算在DRM原則中套用新的使用規則，而且您打算在已封裝為舊版授權伺服器的內容（因此無法正確解譯新的使用規則）中使用此DRM原則，則可能需要指定舊版授權伺服器的運作方式。 預設情況下，DRM策略重要性設定為`true`。

此設定表示許可證伺服器必須處理DRM策略的所有部分，才能生成使用指定DRM策略的許可證。 如果DRM策略重要性設定為`false`，則舊版許可伺服器可能會忽略DRM策略中無法正確解釋的部分。 因此，伺服器產生的任何授權都不包含任何新的使用規則。

Primetime DRM伺服器支援SDK 2.0.2版或更新版本，接受DRM政策重要性設定。
