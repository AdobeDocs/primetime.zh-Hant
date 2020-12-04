---
description: 若要最有效率地使用TVSDK，您應考慮其運作的特定詳細資訊，並遵循特定最佳實務。
seo-description: 若要最有效率地使用TVSDK，您應考慮其運作的特定詳細資訊，並遵循特定最佳實務。
seo-title: 考量事項和最佳實務
title: 考量事項和最佳實務
uuid: e698ae09-280b-4406-a9b8-4f468b7a6b9c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# 考慮事項和最佳做法{#considerations-and-best-practices}

若要最有效率地使用TVSDK，您應考慮其運作的特定詳細資訊，並遵循特定最佳實務。

## 注意事項{#section_tvsdk_considerations}

使用TVSDK時，請記住下列資訊：

* Adobe Primetime目前無法在Android模擬器上運作。

   您必須使用真正的裝置進行測試。
* 僅HTTP即時串流(HLS)內容支援播放。
* 主視頻內容可以被多路復用，其中視頻和音頻流位於相同的轉譯中，或者非多路復用，其中視頻和音頻流位於不同的轉譯中。
* TVSDK API是以Java建置。
* 目前，您必須在UI執行緒（主要Android執行緒）上執行大部分的TVSDK API作業。

   在主線程上正確運行的操作可能會擲出錯誤，並在後台線程上運行時退出。
* 視訊播放需要Adobe視訊引擎(AVE)。 這會影響訪問介質資源的方式和時間：

   * 在AVE提供的範圍內支援隱藏字幕。
   * 根據編碼器精度，實際編碼媒體持續時間可能與串流資源清單中記錄的持續時間不同。

      在理想的虛擬時間軸和實際播放時間軸之間，沒有可靠的方式重新同步。 廣告管理和視訊分析的串流播放進度追蹤必須使用實際播放時間，因此報告和使用者介面行為可能無法精確追蹤媒體和廣告內容。
   * 來自此平台TVSDK之所有媒體要求的傳入使用者代理名稱會指派下列字串模式：

      ```
      "Adobe Primetime/ + 
      <varname>
      originalUserAgent
      </varname>" 
      ```

      如果您在設定廣告插入中繼資料時設定廣告相關呼叫，則所有廣告相關呼叫都會使用Android預設使用者代理或自訂使用者代理。

## 最佳做法{#section_tvsdk_best_practices}

以下是TVSDK的建議實務：

* 使用HLS 3.0版或更新版本來取得程式內容。
* 在主(UI)執行緒中執行大部分的TVSDK作業，而非在背景執行緒中執行。
