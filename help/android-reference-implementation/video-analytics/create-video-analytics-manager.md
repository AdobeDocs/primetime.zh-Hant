---
description: 建立視訊分析管理員
seo-description: 建立視訊分析管理員
seo-title: 建立視訊分析管理員
title: 建立視訊分析管理員
uuid: d72e1dfe-df70-47cc-9e00-bd09017d6127
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '118'
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
>如果Android應用程式未設定Adobe Analytics帳戶，則即使已建立並啟用`VAManager`的例項，也不會產生視訊追蹤資料。

