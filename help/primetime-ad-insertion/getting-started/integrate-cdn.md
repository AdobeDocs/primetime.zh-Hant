---
title: 整合您的CDN
description: 整合您的CDN
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 整合您的CDN {#integrating-cdn}

Primetime廣告插入功能是您用戶端應用程式與資訊清單之間的代理，而非視訊區塊本身。 使用引導API將您的內容部署至所選的CDN，並將URL傳遞至Primetime廣告插入。 如需整合詳細資訊，請參閱[支援的CDN](/help/primetime-ad-insertion/technical-reference/supported-cdns.md)。

## 支援的CDN Token化方案{#cdn-tokenization-schemes}

CDN通常有不同的碎片授權Token化方案。 Primetime廣告插入原生支援主要CDN網路，包括：

* Akamai
* Limelight
* Centurylink / Level3
* 請連絡您的Primetime支援代表，以取得支援CDN的完整清單

有關`pttoken`參數的詳細資訊，請參閱[引導API參數說明](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description)。

## 設定廣告以從內容CDN {#configure-ad-deliver-from-cdn}傳送

您可能想要從相同CDN傳送廣告和內容，以維持內容親和力、協助略過廣告封鎖程式及／或最佳化用戶端應用程式所需連線數目。 Primetime廣告插入支援片段重寫規則，以將片段對應至您的內容CDN。 如需詳細資訊，請參閱[資訊清單重寫](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md)。

## 使用您的CDN {#increase-startup-performance}提高啟動效能

如需詳細資訊，請參閱[最佳化啟動](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md)。

## 多CDN功能{#enable-multi-cdn-fetures}

請連絡您的Primetime支援代表以啟用多CDN功能。
