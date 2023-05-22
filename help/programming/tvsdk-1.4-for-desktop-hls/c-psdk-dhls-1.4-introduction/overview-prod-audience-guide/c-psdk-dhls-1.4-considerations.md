---
description: 要最有效地使用TVSDK，您應考慮其操作的某些詳細資訊並遵循某些最佳實踐。
title: 考慮事項和最佳做法
exl-id: 5e1e09e1-f22e-4797-807a-14dbf50bb835
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 考慮事項和最佳做法{#considerations-and-best-practices}

要最有效地使用TVSDK，您應考慮其操作的某些詳細資訊並遵循某些最佳實踐。

## 注意事項 {#section_tvsdk_considerations}

使用TVSDK時請記住以下資訊：

* Adobe Primetime在模擬器或模擬器上不工作。

   必須使用真實設備進行測試。
* 僅HTTP即時流(HLS)內容支援播放。
* 主視頻內容可以被復用，其中視頻和音頻流處於相同的再現中，或者非復用，其中視頻和音頻流處於不同的再現中。
* TVSDK API是在ActionScript中實現的。
* 視頻播放需要Adobe視頻引擎(AVE)。 這會影響訪問媒體資源的方式和時間：

   * 在AVE提供的範圍內支援隱藏字幕。
   * 根據編碼器精度，實際編碼媒體持續時間可能不同於在流資源清單中記錄的持續時間。

      在理想的虛擬時間線和實際的播放時間線之間沒有重新同步的可靠方法。 對用於廣告管理和視頻分析的流播放的進度跟蹤必須使用實際播放時間，因此報告和用戶介面行為可能無法精確跟蹤媒體和廣告內容。
   * 此平台上TVSDK中所有HTTP請求的傳入用戶代理名稱分配了以下字串模式：

      ```
      "Adobe Flash Player"
      ```

## 最佳做法 {#section_tvsdk_best_practices}

以下是TVSDK的推薦做法：

* 使用HLS 3.0或更高版本來獲取程式內容。
* 對於TVSDK 1.4（用於DHLS），預設情況下啟用懶散載入。

   對於沒有預卷或中卷的內容，您可以 `AdvertisingMetadata.delayAdLoading` 以加快內容載入。
