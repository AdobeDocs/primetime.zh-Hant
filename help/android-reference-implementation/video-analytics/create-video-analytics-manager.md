---
description: 建立視訊分析管理員
seo-description: 建立視訊分析管理員
seo-title: 建立視訊分析管理員
title: 建立視訊分析管理員
uuid: d72e1dfe-df70-47cc-9e00-bd09017d6127
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 建立視訊分析管理員 {#create-the-video-analytics-manager}

Android參考實作中已 `VAManager`新增新的管理器類別()。 `VAManager` 只需建立並銷毀類的實 `VideoHeartbeat` 例。 當建立新實作 `VAManager` 時，參考實作會建 `MediaPlayer` 立例項，並在銷毀該例項時 `MediaPlayer` 銷毀該例項。 這在中實施 `PlayerFragment.java`。

## 若要建立新的視訊分析管理員

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

config變數是執行時期組態的 `IVAConfig` 具體實作 `VideoHeartbeat` 方式。

>[!NOTE]
>
>如果Android應用程式未設定Adobe Analytics帳戶，則即使已建立並啟用例項，也不會產生視訊 `VAManager` 追蹤資料。

