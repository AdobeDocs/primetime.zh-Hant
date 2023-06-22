---
title: DRM政策重要性
description: DRM政策重要性
copied-description: true
exl-id: b9f5a095-9ec4-4ad7-8b70-9abae72d2a86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# DRM政策重要性{#drm-policy-criticality}

如果您計畫在DRM原則中套用新的使用規則，並且如果您計畫在已封裝為舊版授權伺服器的內容中使用此DRM原則（因此不會正確解釋新的使用規則），您可能需要指定舊版授權伺服器的行為方式。 預設情況下，DRM原則重要性設定為 `true`.

此設定表示許可證伺服器必須先處理DRM原則的所有部分，才能產生使用指定DRM原則的許可證。 如果DRM原則重要性設為 `false`，舊版授權伺服器可能會忽略DRM政策中無法正確解讀的部分。 因此，伺服器產生的任何授權不包含任何新的使用規則。

支援SDK 2.0.2版或更新版本的Primetime DRM伺服器接受DRM原則重要性設定。
