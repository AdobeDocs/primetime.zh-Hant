---
description: 當黃金時段對象嘗試播放在回放之前需要用戶憑據進行身份驗證的受保護內容（且尚未執行身份驗證）時，會調度DRMAuthenticateEvent對象。 DRMAuthenticateEvent處理程式負責收集所需的憑據（用戶名、密碼和類型），並將值傳遞到.setDRMAuthenticationCredentials()方法進行驗證。
title: 建立DRMAuthenticateEvent處理程式
exl-id: fe01340b-8a76-4fd4-8c6c-85454d0e2218
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# 建立DRMAuthenticateEvent處理程式{#create-a-drmauthenticateevent-handler}

當黃金時段對象嘗試播放在回放之前需要用戶憑據進行身份驗證的受保護內容（且尚未執行身份驗證）時，會調度DRMAuthenticateEvent對象。 DRMAuthenticateEvent處理程式負責收集所需的憑據（用戶名、密碼和類型），並將值傳遞到.setDRMAuthenticationCredentials()方法進行驗證。

應用程式必須提供一些獲取用戶憑據的機制。 例如，應用程式可以為用戶提供一個簡單的用戶介面來輸入用戶名和密碼值。 此外，它還應提供處理和限制重複驗證失敗嘗試的機制。

建立將一組硬編碼身份驗證憑據傳遞給發起事件的Mighine對象的事件處理程式：

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

（此處不包括用於播放視頻並確保已成功連接到視頻流的代碼。）
