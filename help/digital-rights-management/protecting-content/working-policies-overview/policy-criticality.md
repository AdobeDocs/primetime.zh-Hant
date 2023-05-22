---
title: DRM策略關鍵程度
description: DRM策略關鍵程度
copied-description: true
exl-id: b9f5a095-9ec4-4ad7-8b70-9abae72d2a86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# DRM策略關鍵程度{#drm-policy-criticality}

如果計畫在DRM策略中應用新的使用規則，並且計畫在已打包用於較舊許可證伺服器的內容中使用此DRM策略（因此無法正確解釋新的使用規則），則可能需要指定較舊許可證伺服器需要如何運行。 預設情況下，DRM策略重要性設定為 `true`。

此設定表示許可證伺服器必須處理DRM策略的所有部分，然後才能生成使用指定DRM策略的許可證。 如果DRM策略重要性設定為 `false`，舊版許可證伺服器可能會忽略DRM策略中無法正確解釋的部分。 因此，伺服器生成的任何許可證都不包含任何新的使用規則。

支援SDK版本2.0.2或更高版本的DRM伺服器接受DRM策略關鍵性設定。
