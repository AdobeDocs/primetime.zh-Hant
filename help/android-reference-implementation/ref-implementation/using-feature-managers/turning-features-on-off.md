---
description: 您可以使用管理員工廠開啟或關閉功能，而不需瀏覽程式碼。
title: 使用「管理員工廠」開啟或關閉功能
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 使用「管理員工廠」開啟或關閉功能{#turning-features-on-or-off-using-managerfactory}

您可以使用管理員工廠開啟或關閉功能，而不需瀏覽程式碼。

以下範例中的啟用引數會決定是否使用功能。 如果為false，則會建立特徵管理員，但只提供預設功能給播放器，就像未建立特徵管理員一樣。 如果為true，則會建立功能管理員、啟用功能，且媒體播放器接受設定檔案的輸入。

例如，在 `com.adobe.primetime.reference.ui.player.PlayerFragment.java` 檔案：

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API檔案**： [工廠經理](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
