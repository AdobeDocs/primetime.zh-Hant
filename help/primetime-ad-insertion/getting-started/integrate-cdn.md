---
title: 整合您的CDN
description: 整合您的CDN
exl-id: b93031a2-6e66-4de1-9cf2-b0260f88fe13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 整合您的CDN {#integrating-cdn}

PrimetimeAd Insertion是使用者端應用程式與資訊清單之間的Proxy，而非視訊區塊本身。 將您的內容部署至選擇的CDN，並使用BootstrapAPI將URL傳遞至PrimetimeAd Insertion。 如需整合的詳細資訊，請參閱 [支援的CDN](/help/primetime-ad-insertion/technical-reference/supported-cdns.md).

## 支援的CDN代碼化配置 {#cdn-tokenization-schemes}

CDN經常針對片段授權使用不同的代碼化配置。 PrimetimeAd Insertion原生支援主要的CDN網路，包括：

* Akamai
* 聚光燈
* Centurylink / Level3
* 如需支援的CDN完整清單，請聯絡您的Primetime支援代表

如需更多有關「 」的資訊， `pttoken` 引數，請參閱 [BootstrapAPI引數說明](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## 設定要從內容CDN傳送的廣告 {#configure-ad-deliver-from-cdn}

您可能想要從相同的CDN傳送廣告和內容，以維持內容相似性、協助略過廣告封鎖程式和/或最佳化來自使用者端應用程式的必要連線數量。 PrimetimeAd Insertion支援片段重寫規則，以將片段對應至您的內容CDN。 如需詳細資訊，請參閱 [資訊清單重新寫入](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## 使用CDN提高啟動效能 {#increase-startup-performance}

如需詳細資訊，請參閱 [最佳化啟動](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## 多CDN功能 {#enable-multi-cdn-fetures}

請聯絡您的Primetime支援代表以啟用多CDN功能。
