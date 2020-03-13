---
description: 您可以使用Manager Factory來開啟或關閉功能，而不需執行程式碼。
seo-description: 您可以使用Manager Factory來開啟或關閉功能，而不需執行程式碼。
seo-title: 使用ManagerFactory開啟或關閉功能
title: 使用ManagerFactory開啟或關閉功能
uuid: 385c2707-95f7-4628-8d25-67731151cb6a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 使用ManagerFactory開啟或關閉功能{#turning-features-on-or-off-using-managerfactory}

您可以使用Manager Factory來開啟或關閉功能，而不需執行程式碼。

以下範例中的啟用引數決定是否使用功能。 如果為false，則會建立功能管理員，但僅提供播放器的預設功能，就像未建立功能管理員一樣。 如果為true，則會建立功能管理員、啟用功能，媒體播放器接受來自設定檔的輸入。

例如，在檔案中 `com.adobe.primetime.reference.ui.player.PlayerFragment.java` :

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API檔案**:ManagerFactory [](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)