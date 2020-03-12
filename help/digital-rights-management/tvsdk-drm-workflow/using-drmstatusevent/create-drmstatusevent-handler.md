---
seo-title: 建立DRMStatusEvent處理程式
title: 建立DRMStatusEvent處理程式
uuid: 64f539d9-344c-4372-88b8-c8d098af9dd8
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# 建立DRMStatusEvent處理程式{#create-a-drmstatusevent-handler}

下面的示例建立事件處理程式，該事件處理程式輸出發生事件的Primetime對象的DRM內容狀態資訊。

將事件處理常式新增至指向受保護內容的Primetime物件：

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

