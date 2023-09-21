---
title: DRM政策重要性
description: DRM政策重要性
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# DRM政策重要性{#drm-policy-criticality}

如果您打算在DRM原則中套用新的使用規則，而且如果您打算在已封裝為舊版許可證伺服器的內容中使用此DRM原則（因此不會正確解譯新的使用規則），您可能需要指定舊版許可證伺服器的行為方式。 依預設，DRM政策重要性設為 `true`.

此設定表示許可證伺服器必須先處理DRM原則的所有部分，才能產生使用指定DRM原則的許可證。 如果DRM政策重要性設為 `false`，舊版授權伺服器可能會忽略其無法正確解讀的DRM政策部分。 因此，伺服器產生的任何授權都不包含任何新的使用規則。

支援SDK 2.0.2版或更新版本的Primetime DRM伺服器接受DRM原則重要性設定。
