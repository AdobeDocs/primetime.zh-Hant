---
description: 建立視訊分析管理員
title: 建立視訊分析管理員
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# 建立視訊分析管理員{#create-the-video-analytics-manager}

新的管理器類別(`VAManager`)已新增至Android參考實作。 `VAManager` 只需建立並銷毀類的實 `VideoHeartbeat` 例。當建立新的`MediaPlayer`時，參考實作會建立`VAManager`例項，並在銷毀`MediaPlayer`時銷毀該例項。 這在`PlayerFragment.java`中實施。

## 若要建立新的視訊分析管理員

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

config變數是`IVAConfig`的具體實作，並包含執行時期`VideoHeartbeat`組態。

>[!NOTE]
>
>如果Android應用程式未設定Adobe Analytics帳戶，則視訊追蹤資料將不會產生，即使已建立並啟用`VAManager`的例項亦然。

