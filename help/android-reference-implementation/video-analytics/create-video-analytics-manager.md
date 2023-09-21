---
description: 建立Video Analytics管理員
title: 建立Video Analytics管理員
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 建立Video Analytics管理員 {#create-the-video-analytics-manager}

新的管理員類別( `VAManager`)已新增至Android參考實作。 `VAManager` 只需建立並毀損的例項 `VideoHeartbeat` 類別。 參考實作會建立 `VAManager` 執行個體，當新的 `MediaPlayer` 建立時，會在建立後損毀該執行個體， `MediaPlayer` 已損毀。 這是在中實作 `PlayerFragment.java`.

## 建立新的Video Analytics管理員

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

設定變數是的具體實施 `IVAConfig` 並包含執行階段 `VideoHeartbeat` 設定。

>[!NOTE]
>
>如果Android應用程式未使用Adobe Analytics帳戶設定，則不會產生視訊追蹤資料，即使 `VAManager` 已建立並啟用。
