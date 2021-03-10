---
description: 功能管理員是TVSDK程式庫的包裝函式。
title: 參考實作結構
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# 參考實施結構{#reference-implementation-structure}

功能管理員是TVSDK程式庫的包裝函式。

在Java中，類是以層次結構化的。 例如，`com.adobe.primetime.reference.ui`下的所有UI相關程式碼和所有功能管理員都位於`com.adobe.primetime.reference.manager`下。

Primetime參考實作包含下列套件：

| 封裝 | 說明 |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | 此類別會延伸android.app.Application。 |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | 包含自訂廣告的程式碼。 |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | 包含設定功能管理員所需的介面程式碼。 |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | 包含DRM的輔助類。 |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | 介面、平台和參考資訊的適配器和項目適配器。 同時也包含FeedAdapterFactory、ContentRenditionInfo和XMLParserHelper程式碼。 |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | 提供本地和遠程記錄的類。 |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | 您可以在這裡找到功能管理員以及ManagerFactory。 對於可啟用或停用的可選功能，有兩種功能管理員： <ul><li>一個功能管理器，即功能的名稱，例如CCManager。 此功能管理員已關閉，並提供預設的關閉行為。</li><li>一個功能管理器在功能管理器名稱中附加了On，例如CCManagerOn。 此功能管理員提供啟用功能的范常式式碼。</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | 包含目錄的UI代碼。 |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | 包含記錄檔的UI程式碼。 |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | 包含播放器的UI程式碼。 |
| [com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | 包含設定的UI程式碼。 |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | 包含一般實用程式類。 |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | 包含`HTTP-specific`實用程式類。 |
