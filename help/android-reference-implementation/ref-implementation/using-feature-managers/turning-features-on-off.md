---
description: 使用經理工廠，可以開啟或關閉功能，而無需通過代碼。
title: 使用ManagerFactory開啟或關閉特徵
exl-id: 4e288a6e-80e5-43c1-aba2-374723dd9957
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 使用ManagerFactory開啟或關閉特徵{#turning-features-on-or-off-using-managerfactory}

使用經理工廠，可以開啟或關閉功能，而無需通過代碼。

下面的示例中的啟用參數確定是否使用了該功能。 如果為false，則建立特徵管理器，但僅向播放器提供預設功能，就好像未建立特徵管理器一樣。 如果為true，則建立功能管理器，啟用該功能，媒體播放器接受來自配置檔案的輸入。

例如，在 `com.adobe.primetime.reference.ui.player.PlayerFragment.java` 檔案：

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API文檔**: [經理工廠](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
