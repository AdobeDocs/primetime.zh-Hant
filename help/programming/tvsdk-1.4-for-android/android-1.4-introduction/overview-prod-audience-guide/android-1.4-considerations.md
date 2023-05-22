---
description: 要最有效地使用TVSDK，您應考慮其操作的某些詳細資訊並遵循某些最佳實踐。
title: 考慮事項和最佳做法
exl-id: 28757b1d-8aa5-4172-91ba-6bacf7b5eb22
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 考慮事項和最佳做法{#considerations-and-best-practices}

要最有效地使用TVSDK，您應考慮其操作的某些詳細資訊並遵循某些最佳實踐。

## 注意事項 {#section_tvsdk_considerations}

使用TVSDK時請記住以下資訊：

* Adobe Primetime目前不在Android模擬器上工作。

   必須使用真實設備進行測試。
* 僅HTTP即時流(HLS)內容支援播放。
* 主視頻內容可以被復用，其中視頻和音頻流處於相同的再現中，或者非復用，其中視頻和音頻流處於不同的再現中。
* TVSDK API是在Java中實現的。
* 目前，您需要在UI線程（主Android線程）上運行大多數TVSDK API操作。

   在主線程上正確運行的操作可能會在後台線程上運行時引發錯誤並退出。
* 視頻播放需要Adobe視頻引擎(AVE)。 這會影響訪問媒體資源的方式和時間：

   * 在AVE提供的範圍內支援隱藏字幕。
   * 根據編碼器精度，實際編碼媒體持續時間可能不同於在流資源清單中記錄的持續時間。

      在理想虛擬時間線和實際播放時間線之間沒有重新同步的可靠方法。 對用於廣告管理和視頻分析的流播放的進度跟蹤必須使用實際播放時間，因此報告和用戶介面行為可能無法精確跟蹤媒體和廣告內容。
   * 此平台上TVSDK中所有媒體請求的傳入用戶代理名稱都按以下字串模式分配：

      ```
      "Adobe Primetime/ + 
      <varname>
      originalUserAgent
      </varname>" 
      ```

      如果在設定廣告插入元資料時設定了所有與廣告相關的呼叫，則使用Android預設用戶代理或自定義用戶代理。

## 最佳做法 {#section_tvsdk_best_practices}

以下是TVSDK的推薦做法：

* 使用HLS 3.0或更高版本來獲取程式內容。
* 在主(UI)線程（而不是後台線程）中運行大多數TVSDK操作。
