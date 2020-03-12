---
seo-title: 建立DRMErrorEvent處理程式
title: 建立DRMErrorEvent處理程式
uuid: dde660fc-6899-47d4-97d4-46acda2db262
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# 建立DRMErrorEvent處理程式{#create-a-drmerrorevent-handler}

建立事件處理常式，以處理從Primetime傳送的錯誤事件，當它嘗試播放受保護的內容時遇到錯誤。

通常，當應用程式遇到錯誤時，會執行任意數目的清除工作。 然後，它會通知使用者錯誤並提供解決問題的選項。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

