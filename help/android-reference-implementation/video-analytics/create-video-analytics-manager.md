---
description: 建立視頻分析管理器
title: 建立視頻分析管理器
exl-id: 8d2bbb39-10e2-43e8-8ed3-bc376b3f3cc8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 建立視頻分析管理器 {#create-the-video-analytics-manager}

新的管理器類( `VAManager`)已添加到Android參考實現中。 `VAManager` 只是建立和銷毀實例 `VideoHeartbeat` 類。 引用實現建立 `VAManager` 實例 `MediaPlayer` 建立，並在 `MediaPlayer` 被毀。 這在 `PlayerFragment.java`。

## 建立新視頻分析管理器

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

config變數是 `IVAConfig` 包含運行時 `VideoHeartbeat` 配置。

>[!NOTE]
>
>如果Android應用程式未配置Adobe Analytics帳戶，則即使Android的實例 `VAManager` 建立並啟用。
