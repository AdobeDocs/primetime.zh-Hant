---
title: 建立DRMErrorEvent處理程式
description: 建立DRMErrorEvent處理程式
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 建立DRMErrorEvent處理程式{#create-a-drmerrorevent-handler}

建立事件處理程式，以處理從Mogifle發送的錯誤事件，當它在嘗試播放受保護的內容時遇到錯誤。

通常，當應用程式遇到錯誤時，它會執行任意數量的清理任務。 然後，它通知用戶該錯誤並提供用於解決該問題的選項。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

