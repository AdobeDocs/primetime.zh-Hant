---
description: Adobe® Access™是高價值視聽內容的高級數字權限管理和內容保護解決方案。 使用使用Java API建立的工具，您可以建立策略、將策略應用於包含音頻和視頻內容的檔案以及加密這些檔案。 執行這些任務的高級步驟如下
title: 概述
exl-id: cf081058-9b41-4b09-9258-a7d873799846
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 概述 {#overview}

Adobe® Access™是高價值視聽內容的高級數字權限管理和內容保護解決方案。 使用使用Java API建立的工具，您可以建立策略、將策略應用於包含音頻和視頻內容的檔案以及加密這些檔案。 執行這些任務的高級步驟如下：

1. 使用Java API設定策略屬性和加密參數。
1. 建立描述內容使用角色的策略。 (請參閱 [使用策略](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md))。

   您可以建立任意數量的策略。 大多數用戶建立少量策略並將其應用於許多檔案。

1. 打包媒體檔案。

   在這種背景下， *打包檔案* 即對其加密並應用策略。 (請參閱 [打包媒體檔案](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md)。)

1. 實施許可證伺服器以向用戶頒發許可證。

加密內容現在已準備好進行部署，客戶端可以從伺服器請求許可。

SDK提供Java API來完成這些任務，包括許可證伺服器的參考實現以及基於Java API的命令行工具。 有關資訊，請參見 *使用Adobe訪問參考實現*。

## AdobeAccess 5.2的新增功能 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **外部CEK**:將內容密鑰管理系統(CKMS)整合到DRM許可證服務和內容打包工作流的能力，而不是加密CEK並將其捆綁到內容的元資料中。 請參閱 [Adobe訪問DRM外部CEK概述](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)。

* **許可證（憑證）退貨**:客戶端返回（或刪除）發給客戶端的許可證的能力。
* **Xbox密鑰伺服器**:能夠保護髮送到Xbox和Xbox 360的內容。 (需要Adobe Primetime客戶。)

## 自定義用法規則 {#custom-usage-rules}

指定自定義用法規則。 自定義資料可以包含在許可證伺服器頒發的許可證中。 該資料的解釋/處理完全取決於客戶端應用和許可證伺服器的實現。

示例用例：通過允許將其他業務規則安全地作為策略和/或內容許可證的一部分傳送，實現使用規則的可擴充性。 出於安全原因，由於這些使用規則是在自定義客戶端應用程式碼中強制實施的，因此此選項應與AIR應用程式或Flash PlayerSWF允許清單選項一起使用。 有關詳細資訊，請參見 [運行時和應用程式限制](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md)。
