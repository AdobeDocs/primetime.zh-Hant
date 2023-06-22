---
title: 建立DRMErrorEvent處理常式
description: 建立DRMErrorEvent處理常式
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 建立DRMErrorEvent處理常式{#create-a-drmerrorevent-handler}

建立事件處理常式，在嘗試播放受保護內容時遇到錯誤時，處理從Primetime傳送的錯誤事件。

通常，當應用程式遇到錯誤時，它會執行任意數量的清理任務。 然後它會通知使用者該錯誤，並提供解決問題的選項。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

