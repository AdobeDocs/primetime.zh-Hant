---
title: 使用DRMErrorEvent類概述
description: 使用DRMErrorEvent類概述
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# 使用DRMErrorEvent類概述 {#using-the-drmerrorevent-class-overview}

黃金時段發稿 `DRMErrorEvent` 當試圖播放受保護內容的黃金時段對象遇到 [與DRM相關的錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。 如果用戶憑據無效， `DRMAuthenticateEvent` 對象重複派單，直到用戶輸入有效憑據或應用程式拒絕進一步嘗試。 應用程式負責偵聽任何其它DRM錯誤事件，以檢測、識別和處理 [與DRM相關的錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。

即使使用有效的用戶憑據，內容許可證的條款仍然可以阻止用戶查看加密內容。 例如，可以拒絕用戶嘗試查看未授權應用程式中的內容的訪問（例如，「應用程式允許清單」）。 未授權的應用程式是尚未使用允許列出的應用程式簽名證書籤名的應用程式。 在這種情況下， `DRMErrorEvent` 對象已調度。

如果內容已損壞或應用程式的版本與許可證指定的版本不匹配，也可以觸發錯誤事件。 應用程式必須提供適當的錯誤處理機制。
