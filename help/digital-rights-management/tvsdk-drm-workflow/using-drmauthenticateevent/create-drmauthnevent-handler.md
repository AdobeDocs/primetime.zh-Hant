---
description: 當Primetime物件嘗試播放需要使用者憑證才能進行驗證的受保護內容時（且尚未執行驗證），就會傳送DRMAuthenticateEvent物件。 DRMAuthenticateEvent處理常式負責收集必要的憑證（使用者名稱、密碼和類型），並將值傳遞至。setDRMAuthenticationCredentials()方法以進行驗證。
seo-description: 當Primetime物件嘗試播放需要使用者憑證才能進行驗證的受保護內容時（且尚未執行驗證），就會傳送DRMAuthenticateEvent物件。 DRMAuthenticateEvent處理常式負責收集必要的憑證（使用者名稱、密碼和類型），並將值傳遞至。setDRMAuthenticationCredentials()方法以進行驗證。
seo-title: 建立DRMAuthenticateEvent處理程式
title: 建立DRMAuthenticateEvent處理程式
uuid: 58330691-d0b5-46bd-9b1d-8dc597580d31
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# 建立DRMAuthenticateEvent處理程式{#create-a-drmauthenticateevent-handler}

當Primetime物件嘗試播放需要使用者憑證才能進行驗證的受保護內容時（且尚未執行驗證），就會傳送DRMAuthenticateEvent物件。 DRMAuthenticateEvent處理常式負責收集必要的憑證（使用者名稱、密碼和類型），並將值傳遞至。setDRMAuthenticationCredentials()方法以進行驗證。

應用程式必須提供一些機制來取得使用者憑證。 例如，應用程式可提供使用者簡單的使用者介面，以輸入使用者名稱和密碼值。 此外，它還應提供處理和限制重複驗證失敗嘗試的機制。

建立事件處理常式，將一組硬式編碼驗證憑證傳遞至產生事件的Primetime物件：

```
var connection:NetConnection = new NetConnection();  
connection.connect(null);  
var videoStream:Primetime = new Primetime(connection);  
 
videoStream.addEventListener( 
  DRMAuthenticateEvent.DRM_AUTHENTICATE,  
  drmAuthenticateEventHandler)  
  private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void {  
    videoStream.setDRMAuthenticationCredentials("administrator", "password", "drm");  
} 
```

（此處未包含用於播放視訊並確保已成功連線至視訊串流的程式碼。）
