---
title: 建立DRMStatusEvent處理程式
description: 建立DRMStatusEvent處理程式
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# 建立DRMStatusEvent處理程式{#create-a-drmstatusevent-handler}

下面的示例建立事件處理程式，該事件處理程式輸出發生事件的Primetime對象的DRM內容狀態資訊。

將事件處理常式新增至指向受保護內容的Primetime物件：

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

