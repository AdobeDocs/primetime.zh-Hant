---
description: 當Primetime物件嘗試播放受保護內容時，會傳送DRMAuthenticateEvent物件，而受保護內容需要在播放前進行驗證的使用者認證（且尚未執行驗證）。 DRMAuthenticationEvent處理常式負責收集所需的認證（使用者名稱、密碼和型別），並將值傳遞至.setDRMAuthenticationCredentials()方法進行驗證。
title: 建立DRMAuthenticateEvent處理常式
exl-id: fe01340b-8a76-4fd4-8c6c-85454d0e2218
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# 建立DRMAuthenticateEvent處理常式{#create-a-drmauthenticateevent-handler}

當Primetime物件嘗試播放受保護內容時，會傳送DRMAuthenticateEvent物件，而受保護內容需要在播放前進行驗證的使用者認證（且尚未執行驗證）。 DRMAuthenticationEvent處理常式負責收集所需的認證（使用者名稱、密碼和型別），並將值傳遞至.setDRMAuthenticationCredentials()方法進行驗證。

應用程式必須提供某種機制來取得使用者認證。 例如，應用程式可為使用者提供簡單的使用者介面，以輸入使用者名稱和密碼值。 此外，它應提供一種機制，用於處理和限制重複的驗證失敗嘗試。

建立事件處理常式，將一組硬式編碼的驗證認證傳遞至產生事件的Primetime物件：

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

（播放視訊並確保成功連線至視訊資料流的程式碼不在此列。）
