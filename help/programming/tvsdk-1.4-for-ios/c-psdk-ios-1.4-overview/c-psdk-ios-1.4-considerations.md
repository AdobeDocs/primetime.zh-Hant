---
description: 要最有效地使用TVSDK，您應考慮其操作的某些詳細資訊並遵循某些最佳實踐。
title: 考慮事項和最佳做法
exl-id: d10532a5-bf96-4233-86f1-b135f6e1c0f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# 考慮事項和最佳做法{#considerations-and-best-practices}

要最有效地使用TVSDK，您應考慮其操作的某些詳細資訊並遵循某些最佳實踐。

## 注意事項 {#section_tvsdk_considerations}

使用TVSDK時請記住以下資訊：

* Adobe Primetime在iOS模擬器上不工作。

   必須使用真實設備進行測試。
* 僅HTTP即時流(HLS)內容支援播放。
* 主視頻內容可以被復用，其中視頻和音頻流處於相同的再現中，或者非復用，其中視頻和音頻流處於不同的再現中。
* TVSDK API在Objective-C中實現。
* 視頻播放需要本機的AppleAV Foundation框架。 這會影響媒體資源（包括隱藏字幕和時間表）的訪問方式和訪問時間：

   * 在初始設定後無法修訂時間線調整。

      例如，播放播發後，無法從時間軸中刪除播發。 如果用戶在演示文稿中尋找回來，則即使策略是刪除廣告，也會再次播放同一廣告。
   * 根據編碼器精度，實際編碼媒體持續時間可能不同於在流資源清單中記錄的持續時間。

      在理想的虛擬時間線和實際的播放時間線之間沒有重新同步的可靠方法。 對用於廣告管理和視頻分析的流播放的進度跟蹤必須使用實際播放時間，因此報告和用戶介面行為可能無法精確跟蹤媒體和廣告內容。
   * 來自此平台上TVSDK的所有HTTP請求的傳入用戶代理由設備和設備上運行的iOS版本確定。

      用戶代理字串的值預設為作業系統分配的值。

## 最佳做法 {#section_tvsdk_best_practices}

以下是TVSDK的推薦做法：

* 使用HLS 3.0或更高版本來獲取程式內容。
* 使用Apple的媒體流驗證工具驗證VOD流。
* 的 `PTSDKConfig` 類提供了對Mighine廣告決策、DRM和Video Analytics伺服器發出的請求強制執行SSL的方法。

   有關詳細資訊，請參見 `forceHTTPS` 和 `isForcingHTTPS` 類中的方法。

   >[!IMPORTANT]
   >
   >不會修改對第三方域（如Ad Tracking像素、內容和Ad URL）的請求以及類似的請求。 內容提供商和廣告伺服器有責任提供通過HTTPS支援的URL。
