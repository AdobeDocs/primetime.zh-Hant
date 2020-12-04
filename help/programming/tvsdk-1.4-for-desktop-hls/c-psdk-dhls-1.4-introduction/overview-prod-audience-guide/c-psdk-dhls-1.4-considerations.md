---
description: 若要最有效率地使用TVSDK，您應考慮其運作的特定詳細資訊，並遵循特定最佳實務。
seo-description: 若要最有效率地使用TVSDK，您應考慮其運作的特定詳細資訊，並遵循特定最佳實務。
seo-title: 考量事項和最佳實務
title: 考量事項和最佳實務
uuid: 62a5d641-6f37-4e4d-bbc2-414bf3681d9c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# 考慮事項和最佳做法{#considerations-and-best-practices}

若要最有效率地使用TVSDK，您應考慮其運作的特定詳細資訊，並遵循特定最佳實務。

## 注意事項{#section_tvsdk_considerations}

使用TVSDK時，請記住下列資訊：

* Adobe Primetime無法用於模擬器或模擬器。

   您必須使用真正的裝置進行測試。
* 僅HTTP即時串流(HLS)內容支援播放。
* 主視頻內容可以被多路復用，其中視頻和音頻流位於相同的轉譯中，或者非多路復用，其中視頻和音頻流位於不同的轉譯中。
* TVSDK API是在ActionScript中實作。
* 視訊播放需要Adobe視訊引擎(AVE)。 這會影響訪問介質資源的方式和時間：

   * 在AVE提供的範圍內支援隱藏字幕。
   * 根據編碼器精度，實際編碼媒體持續時間可能與串流資源清單中記錄的持續時間不同。

      在理想的虛擬時間軸和實際播放時間軸之間沒有可靠的重新同步方法。 廣告管理和視訊分析的串流播放進度追蹤必須使用實際播放時間，因此報告和使用者介面行為可能無法精確追蹤媒體和廣告內容。
   * 此平台上來自TVSDK的所有HTTP要求的傳入使用者代理名稱會指派下列字串模式：

      ```
      "Adobe Flash Player"
      ```

## 最佳做法{#section_tvsdk_best_practices}

以下是TVSDK的建議實務：

* 使用HLS 3.0版或更新版本來取得程式內容。
* 對於DHLS的TVSDK 1.4，預設會啟用延遲廣告載入。

   對於沒有前置或中置的內容，您可以使用`AdvertisingMetadata.delayAdLoading`來加速內容載入。

