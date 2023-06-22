---
title: 建立DRMStatusEvent處理常式
description: 建立DRMStatusEvent處理常式
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# 建立DRMStatusEvent處理常式{#create-a-drmstatusevent-handler}

下列範例會建立事件處理常式，輸出產生事件之Primetime物件的DRM內容狀態資訊。

將事件處理常式新增至指向受保護內容的Primetime物件：

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

