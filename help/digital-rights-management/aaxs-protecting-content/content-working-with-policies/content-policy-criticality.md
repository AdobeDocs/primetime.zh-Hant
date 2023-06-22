---
title: 原則重要性
description: 原則重要性
copied-description: true
exl-id: 6c6971fe-0c0a-4998-917c-aebbf1c4a9df
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 原則重要性{#policy-criticality}

如果在原則中使用新的使用規則，並且這些原則用於封裝舊版授權伺服器的內容中（這些伺服器不瞭解新的使用規則），您可以指定舊版授權伺服器的行為方式。 依預設，原則重要性為「true」，表示授權伺服器必須瞭解原則的所有部分，才能使用原則產生授權。 如果原則重要性設為「false」，舊版授權伺服器可能會忽略它不瞭解的部分原則，而且伺服器產生的授權不會包含新的使用規則。

使用SDK 2.0.2版及更新版本的Adobe存取伺服器將遵循原則重要性設定。
