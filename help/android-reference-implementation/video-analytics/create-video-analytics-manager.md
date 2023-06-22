---
description: 建立Video Analytics管理員
title: 建立Video Analytics管理員
exl-id: 8d2bbb39-10e2-43e8-8ed3-bc376b3f3cc8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 建立Video Analytics管理員 {#create-the-video-analytics-manager}

新的管理員類別( `VAManager`)已新增至Android參考實作。 `VAManager` 只需建立並損毀 `VideoHeartbeat` 類別。 參考實作會建立 `VAManager` 執行個體何時新 `MediaPlayer` 建立時，會破壞該執行個體，當 `MediaPlayer` 已損毀。 這是在中實作 `PlayerFragment.java`.

## 若要建立新的Video Analytics管理員

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

config變數是的具體實施 `IVAConfig` 並包含執行階段 `VideoHeartbeat` 設定。

>[!NOTE]
>
>如果Android應用程式未使用Adobe Analytics帳戶設定，則不會產生視訊追蹤資料，即使 `VAManager` 建立並啟用。
