---
description: 'Adobe® Access™是高價值視訊內容的進階數位版權管理與內容保護解決方案。 使用您使用Java API建立的工具，您可以建立原則、將原則套用至包含音訊和視訊內容的檔案，以及加密這些檔案。 執行這些任務的高級步驟如下 '
seo-description: 'Adobe® Access™是高價值視訊內容的進階數位版權管理與內容保護解決方案。 使用您使用Java API建立的工具，您可以建立原則、將原則套用至包含音訊和視訊內容的檔案，以及加密這些檔案。 執行這些任務的高級步驟如下 '
seo-title: 概觀
title: 概觀
uuid: 874c175b-8207-49fa-aad4-204ccbee9c2c
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# 概觀 {#overview}

Adobe® Access™是高價值視訊內容的進階數位版權管理與內容保護解決方案。 使用您使用Java API建立的工具，您可以建立原則、將原則套用至包含音訊和視訊內容的檔案，以及加密這些檔案。 執行這些任務的高級步驟如下：

1. 使用Java API來設定原則屬性和加密參數。
1. 建立描述內容使用角色的原則。 (請參 [閱使用策略](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md))。

   您可以建立任意數量的策略。 大多數用戶建立少量策略並將其應用於多個檔案。

1. 封裝媒體檔案。

   在此上下文中， *打包檔案* 意味著加密檔案並對其應用策略。 (請參閱 [封裝媒體檔案](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md)。)

1. 實作授權伺服器，以向使用者發放授權。

加密的內容現在已可供部署，而且用戶端可向伺服器要求授權。

SDK提供Java API來完成這些工作，並包含授權伺服器的參考實作，以及以Java API為基礎的命令列工具。 如需詳細資訊，請 *參閱使用Adobe存取參考實作*。

## Adobe Access 5.2的新增功能 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **外部CEK**: 將內容密鑰管理系統(CKMS)整合至DRM授權服務和內容封裝工作流程的能力，而不是加密CEK並將它捆綁在內容的中繼資料中。 請參 [閱Adobe Access DRM External CEK概觀](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)。

* **授權（憑單）退貨**: 用戶端可傳回（或刪除）發給用戶端的授權。
* **Xbox Key Server**: 能夠保護傳送至Xbox和Xbox 360的內容。 （需要Adobe Primetime用戶端。）

## 自訂使用規則 {#custom-usage-rules}

指定自訂使用規則。 自訂資料可包含在授權伺服器核發的授權中。 此資料的解譯／處理完全由用戶端應用程式和授權伺服器的實作決定。

範例使用案例： 允許將其他商業規則安全地傳達為原則及／或內容授權的一部分，以擴充使用規則。 出於安全原因，由於這些使用規則是在自訂用戶端應用程式碼中強制執行的，因此應搭配AIR應用程式或Flash Player SWF允許清單選項使用此選項。 如需詳細資訊，請參閱「執 [行時期和應用程式限制](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md)」。
