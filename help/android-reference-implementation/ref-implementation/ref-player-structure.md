---
description: 功能管理器用作TVSDK庫的包裝。
title: 參考實現結構
exl-id: cf102ccc-2e31-4197-a321-e485f77ba754
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# 參考實現結構 {#reference-implementation-structure}

功能管理器用作TVSDK庫的包裝。

在Java中，類是按層次結構的。 例如，下面所有與UI相關的代碼 `com.adobe.primetime.reference.ui` 所有功能管理器都位於 `com.adobe.primetime.reference.manager`。

黃金時段參考實現包含以下包：

| 包 | 說明 |
|--- |--- |
| [com.adobe.mogife.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | 此類擴展了android.app.Application。 |
| [com.adobe.mighipe.reference.afderting](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | 包含自定義廣告的代碼。 |
| [com.adobe.magifie.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | 包含配置功能管理器所需的介面代碼。 |
| [com.adobe.mighipe.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | 包含DRM的幫助程式類。 |
| [com.adobe.mogifie.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | 介面、平台和參考資訊的適配器和項目適配器。 還包括FeedAdapterFactory、ContentRenditionInfo和XMLParserHelper代碼。 |
| [com.adobe.mighipe.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | 提供本地和遠程日誌記錄的類。 |
| [com.adobe.mogifie.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | 在此處可以找到特徵管理器和ManagerFactory。 對於可啟用或禁用的可選功能，有兩個功能管理器： <ul><li>一個特徵管理器，即特徵的名稱，例如CCManager。 此功能管理器已關閉，並提供預設關閉行為。</li><li>一個特徵管理器，它已附加到特徵管理器名稱，例如CCManagerOn。 此功能管理器為啟用的功能提供示例代碼。</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | 包含目錄的UI代碼。 |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | 包含日誌的UI代碼。 |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | 包含播放器的UI代碼。 |
| [com.adobe.primetime.reference.ui.se](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | 包含設定的UI代碼。 |
| [com.adobe.migfire.reference.utis](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | 包含常規實用程式類。 |
| [com.adobe.with.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | 包含 `HTTP-specific` 實用程式類。 |
