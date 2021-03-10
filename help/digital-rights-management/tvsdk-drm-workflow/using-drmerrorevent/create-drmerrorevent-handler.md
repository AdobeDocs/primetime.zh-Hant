---
title: 建立DRMErrorEvent處理程式
description: 建立DRMErrorEvent處理程式
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 建立DRMErrorEvent處理程式{#create-a-drmerrorevent-handler}

建立事件處理常式，以處理從Primetime傳送的錯誤事件，當它嘗試播放受保護的內容時遇到錯誤。

通常，當應用程式遇到錯誤時，會執行任意數目的清除工作。 然後，它會通知使用者錯誤並提供解決問題的選項。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

