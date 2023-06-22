---
title: 使用DRMErrorEvent類別概觀
description: 使用DRMErrorEvent類別概觀
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# 使用DRMErrorEvent類別概觀 {#using-the-drmerrorevent-class-overview}

Primetime會傳送 `DRMErrorEvent` 物件（當Primetime物件嘗試播放受保護內容時） [DRM相關錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). 如果使用者認證無效， `DRMAuthenticateEvent` 物件會重複傳送，直到使用者輸入有效憑證或應用程式拒絕進一步嘗試為止。 應用程式負責監聽任何其他DRM錯誤事件，以偵測、識別及處理 [DRM相關錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

即使使用有效的使用者憑證，內容授權的條款仍可能阻止使用者檢視加密的內容。 例如，使用者嘗試在未經授權的應用程式中檢視內容（例如應用程式允許清單）時，可能會被拒絕存取。 未獲授權的應用程式是指尚未使用允許列出的應用程式簽署憑證簽署的應用程式。 在此案例中， `DRMErrorEvent` 物件已分派。

如果內容損毀或應用程式的版本不符合授權所指定的內容，也會觸發錯誤事件。 應用程式必須提供處理錯誤的適當機制。
