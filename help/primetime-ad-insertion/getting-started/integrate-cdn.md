---
title: 整合您的CDN
description: 整合CDN
exl-id: b93031a2-6e66-4de1-9cf2-b0260f88fe13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 整合您的CDN {#integrating-cdn}

黃金時段Ad Insertion是客戶端應用程式和清單之間的代理，而不是視頻塊本身。 將您的內容部署到選擇的CDN，並使用BootstrapAPI將URL傳遞到黃金時段Ad Insertion。 有關整合詳細資訊，請參閱 [支援的CDN](/help/primetime-ad-insertion/technical-reference/supported-cdns.md)。

## 支援的CDN令牌化方案 {#cdn-tokenization-schemes}

CDN通常有不同的碎片授權標籤方案。 黃金時段Ad Insertion本機支援主要CDN網路，包括：

* 阿卡邁
* 聚光燈
* Centurylink /級別3
* 請聯繫您的黃金時段支援代表，以獲得受支援CDN的完整清單

有關 `pttoken` 參數，請參閱 [BootstrapAPI參數說明](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description)。

## 配置要從內容CDN傳遞的廣告 {#configure-ad-deliver-from-cdn}

您可能希望從同一CDN傳遞廣告和內容，以維護內容關聯性，幫助繞過廣告攔截器和/或優化客戶端應用程式所需的連接數。 黃金時段Ad Insertion支援片段重寫規則，以將片段映射到內容CDN。 有關詳細資訊，請參見 [清單重寫](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md)。

## 使用您的CDN提高啟動效能 {#increase-startup-performance}

有關詳細資訊，請參見 [優化啟動](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md)。

## 多CDN功能 {#enable-multi-cdn-fetures}

聯繫您的黃金時段支援代表以啟用多CDN功能。
