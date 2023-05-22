---
title: 使用DRMErrorEvent類概述
description: 使用DRMErrorEvent類概述
copied-description: true
exl-id: c651cdcf-f8f8-4085-a88e-d82030f90f11
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 使用DRMErrorEvent類 {#using-the-drmerrorevent-class}

黃金時段發稿 `DRMErrorEvent` 當試圖播放受保護內容的黃金時段對象遇到 [與DRM相關的錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。 如果用戶憑據無效， `DRMAuthenticateEvent` 對象重複派單，直到用戶輸入有效憑據或應用程式拒絕進一步嘗試。 應用程式負責偵聽任何其它DRM錯誤事件，以檢測、識別和處理 [與DRM相關的錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。

即使使用有效的用戶憑據，內容許可證的條款仍然可以阻止用戶查看加密內容。 例如，可以拒絕用戶嘗試查看未授權應用程式中的內容的訪問（例如，「應用程式允許清單」）。 未授權的應用程式是尚未使用允許列出的應用程式簽名證書籤名的應用程式。 在這種情況下， `DRMErrorEvent` 對象已調度。

如果內容已損壞或應用程式的版本與許可證指定的版本不匹配，也可以觸發錯誤事件。 應用程式必須提供適當的錯誤處理機制。

## 建立DRMErrorEvent處理程式 {#create-a-drmerrorevent-handler}

建立事件處理程式，以處理從Mogifle發送的錯誤事件，當它在嘗試播放受保護的內容時遇到錯誤。

通常，當應用程式遇到錯誤時，它會執行任意數量的清理任務。 然後，它通知用戶該錯誤並提供用於解決該問題的選項。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
