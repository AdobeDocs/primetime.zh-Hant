---
description: Adobe® Access™是適用於高價值視聽內容的進階數位版權管理和內容保護解決方案。 使用您使用Java API建立的工具，您可以建立原則、將原則套用至包含音訊和視訊內容的檔案，並加密這些檔案。 執行這些工作的高層級步驟如下
title: 概觀
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 概觀 {#overview}

Adobe® Access™是適用於高價值視聽內容的進階數位版權管理和內容保護解決方案。 使用您使用Java API建立的工具，您可以建立原則、將原則套用至包含音訊和視訊內容的檔案，並加密這些檔案。 執行這些工作的高層級步驟如下：

1. 使用Java API來設定原則屬性和加密引數。
1. 建立說明內容之使用角色的原則。 (請參閱 [使用原則](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md))。

   您可以建立任意數量的原則。 大部分使用者會建立少量原則，並將這些原則套用至許多檔案。

1. 封裝媒體檔案。

   在此內容中， *封裝檔案* 表示要加密並套用原則。 (請參閱 [正在封裝媒體檔案](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. 實作授權伺服器以核發授權給使用者。

加密內容現在已準備好進行部署，使用者端可以從伺服器要求授權。

SDK提供Java API來完成這些工作，並包含授權伺服器的參考實作，以及以Java API為基礎的命令列工具。 如需詳細資訊，請參閱 *使用Adobe存取參考實作*.

## Adobe存取5.2的新增功能 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **外部CEK**：能夠將內容金鑰管理系統(CKMS)整合到DRM授權服務和內容封裝工作流程，而不是加密CEK並將其繫結到內容的中繼資料。 另請參閱 [Adobe存取DRM外部CEK概述](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **授權（憑單）退貨**：使用者端傳回（或刪除）已核發至使用者端的授權的能力。
* **Xbox Key Server**：保護傳送至Xbox和Xbox 360之內容的能力。 (需要Adobe Primetime使用者端。)

## 自訂使用規則 {#custom-usage-rules}

指定自訂使用規則。 自訂資料可包含在授權伺服器發行的授權中。 此資料的解釋/處理完全取決於使用者端應用程式和授權伺服器的實作。

使用案例範例：透過允許作為原則和/或內容授權的一部分安全地傳送其他商業規則，啟用使用規則的擴充性。 基於安全性理由，因為這些使用規則是在自訂使用者端應用程式程式碼中強制執行，所以此選項應與AIR應用程式或Flash PlayerSWF允許清單選項搭配使用。 如需詳細資訊，請參閱 [執行階段和應用程式限制](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
