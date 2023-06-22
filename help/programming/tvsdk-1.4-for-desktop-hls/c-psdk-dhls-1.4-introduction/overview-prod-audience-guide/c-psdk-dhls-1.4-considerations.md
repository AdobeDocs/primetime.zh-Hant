---
description: 若要以最有效的方式使用TVSDK，您應考慮其運作的特定細節，並遵循某些最佳實務。
title: 考量事項和最佳作法
exl-id: 5e1e09e1-f22e-4797-807a-14dbf50bb835
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 考量事項和最佳作法{#considerations-and-best-practices}

若要以最有效的方式使用TVSDK，您應考慮其運作的特定細節，並遵循某些最佳實務。

## 考量事項 {#section_tvsdk_considerations}

使用TVSDK時，請記住下列資訊：

* Adobe Primetime無法用於模擬器或模擬器。

   您必須使用真實裝置進行測試。
* 僅HTTP即時資料流(HLS)內容支援播放。
* 主要視訊內容可以多工處理，其中視訊和音訊資料流位於相同的轉譯中；也可以非多工處理，其中視訊和音訊資料流位於不同的轉譯中。
* TVSDK API已實作ActionScript。
* 視訊播放需要Adobe Video Engine (AVE)。 這會影響存取媒體資源的方式和時間：

   * AVE提供的範圍內支援隱藏式字幕。
   * 根據編碼器精確度，實際的編碼媒體持續時間可能與串流資源資訊清單中記錄的持續時間不同。

      在理想的虛擬時間軸和實際的播放時間軸之間，沒有可靠的方法可重新同步。 廣告管理和視訊分析的串流播放進度追蹤必須使用實際播放時間，因此報告和使用者介面行為可能無法準確追蹤媒體和廣告內容。
   * 來自此平台TVSDK之所有HTTP要求的傳入使用者代理程式名稱會指派以下字串模式：

      ```
      "Adobe Flash Player"
      ```

## 最佳實務 {#section_tvsdk_best_practices}

以下是TVSDK的建議作法：

* 針對程式內容使用HLS 3.0版或更新版本。
* TVSDK 1.4 for DHLS預設會啟用延遲廣告載入。

   對於沒有前段或中段的內容，您可以使用 `AdvertisingMetadata.delayAdLoading` 以加速內容載入。
