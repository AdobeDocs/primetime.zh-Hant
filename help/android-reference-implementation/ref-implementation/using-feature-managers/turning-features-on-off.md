---
description: 您可以使用管理員工廠開啟或關閉功能，而不需瀏覽程式碼。
title: 使用ManagerFactory開啟或關閉功能
exl-id: 4e288a6e-80e5-43c1-aba2-374723dd9957
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 使用ManagerFactory開啟或關閉功能{#turning-features-on-or-off-using-managerfactory}

您可以使用管理員工廠開啟或關閉功能，而不需瀏覽程式碼。

以下範例中的enablement引數會決定是否使用功能。 如果為false，則會建立特徵管理員，但只提供預設功能給播放器，就像未建立特徵管理員一樣。 如果為true，則會建立功能管理員、啟用功能，且媒體播放器會接受設定檔案的輸入。

例如，在 `com.adobe.primetime.reference.ui.player.PlayerFragment.java` 檔案：

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API檔案**： [Managerfactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
