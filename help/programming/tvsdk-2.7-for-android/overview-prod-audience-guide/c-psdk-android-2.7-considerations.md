---
description: 為了以最有效的方式使用TVSDK，您應考慮其操作的特定細節，並遵循某些最佳實務。
title: 考量事項和最佳作法
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 考量事項和最佳作法{#considerations-and-best-practices}

為了以最有效的方式使用TVSDK，您應考慮其操作的特定細節，並遵循某些最佳實務。

## 考量事項 {#section_tvsdk_considerations}

使用TVSDK時，請記住下列資訊：

* TVSDK API實作於Java。
* Adobe Primetime目前無法在Android模擬器上運作。

  您必須使用真實裝置進行測試。
* 僅HTTP即時資料流(HLS)內容支援播放。
* 主要視訊內容可以多工（相同轉譯中的視訊和音訊資料流）或非多工（不同轉譯中的視訊和音訊資料流）。
* 目前，您需要在使用者介面對話串（主要Android對話串）上執行大多數TVSDK API操作。

  在主執行緒上正確執行的作業會在背景執行緒上執行時，擲回錯誤並結束。
* 視訊播放需要Adobe Video Engine (AVE)。 這會影響存取媒體資源的方式和時間：

   * AVE提供的範圍內支援隱藏式字幕。
   * 視編碼器精確度而定，實際的編碼媒體持續時間可能與資料流資源資訊清單中記錄的持續時間不同。

     在理想的虛擬時間軸和實際的播放時間軸之間，沒有可靠的重新同步方式。 廣告管理和視訊分析的串流播放進度追蹤必須使用實際播放時間，因此報告和使用者介面行為可能無法準確追蹤媒體和廣告內容。
   * 來自此平台TVSDK之所有媒體請求的傳入使用者代理名稱會指派以下字串模式：

  ```
  "Adobe Primetime/" + 
  <varname>
  originalUserAgent
  </varname> 
  ```

  如果您在設定廣告插入中繼資料時設定Android預設使用者代理或自訂使用者代理，則所有與廣告相關的呼叫都會使用。

## 最佳實務 {#section_tvsdk_best_practices}

以下是TVSDK的建議作法：

* 針對程式內容使用HLS 3.0版或更高版本。
* 在主(UI)執行緒而不是背景執行緒上執行大多數TVSDK操作。
* 對於適用於Android的TVSDK 2.5，預設會開啟延遲廣告解析。

  對於沒有前段或中段的內容，您可以使用 `AdvertisingMetadata.setPreroll(false)` 以加速內容載入。
