---
seo-title: 使用DRMErrorEvent類概述
title: 使用DRMErrorEvent類概述
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# 使用DRMErrorEvent類{#using-the-drmerrorevent-class}

當Primetime物件嘗試播放受保護的內容時，Primetime會調度`DRMErrorEvent`物件，遇到[DRM相關錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。 如果用戶憑據無效，則`DRMAuthenticateEvent`對象會重複派單，直到用戶輸入有效憑據或應用程式拒絕進一步嘗試為止。 該應用程式負責監聽任何其它DRM錯誤事件，以檢測、識別和處理[DRM相關錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。

即使使用有效的使用者憑證，內容授權的條款仍可能阻止使用者檢視加密內容。 例如，當使用者嘗試檢視未授權應用程式中的內容時，可能會被拒絕存取（例如「應用程式允許」清單）。 未授權的應用程式是指尚未使用允許列出的應用程式簽署憑證進行簽署的應用程式。 在這種情況下，會調度`DRMErrorEvent`對象。

如果內容損毀或應用程式的版本不符合授權所指定的版本，也可引發錯誤事件。 應用程式必須提供適當的機制來處理錯誤。

## 建立DRMErrorEvent處理程式{#create-a-drmerrorevent-handler}

建立事件處理常式，以處理從Primetime傳送的錯誤事件，當它嘗試播放受保護的內容時遇到錯誤。

通常，當應用程式遇到錯誤時，會執行任意數目的清除工作。 然後，它會通知使用者錯誤並提供解決問題的選項。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
