---
description: 若要以最有效的方式使用TVSDK，您應考慮其運作的特定細節，並遵循某些最佳實務。
title: 考量事項和最佳作法
exl-id: f5d3e0ff-675f-4bd4-bfda-71988d25c85d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 考量事項和最佳作法 {#considerations-and-best-practices}

若要以最有效的方式使用TVSDK，您應考慮其運作的特定細節，並遵循某些最佳實務。

## 考量事項 {#section_tvsdk_considerations}

使用TVSDK時，請記住下列資訊：

* Adobe Primetime無法在iOS模擬器上運作。

   您必須使用真實裝置進行測試。

* 僅HTTP即時資料流(HLS)內容支援播放。

* 主要視訊內容可以多工處理，其中視訊和音訊資料流位於相同的轉譯中，也可以非多工處理，其中視訊和音訊資料流位於不同的轉譯中。

* TVSDK API是在Objective-C中實作。

* 視訊播放需要原生Apple AV Foundation架構。 這會影響存取媒體資源（包括隱藏式字幕和時間表）的方式和時間：

   * 在初始設定後，無法修訂時間表調整。

      例如，廣告播放後即無法從時間軸移除。 如果使用者在簡報中搜尋回來，即使原則是移除廣告，也會再次播放相同的廣告。

   * 根據編碼器精確度，實際的編碼媒體持續時間可能與串流資源資訊清單中記錄的持續時間不同。

      在理想的虛擬時間軸和實際的播放時間軸之間，沒有可靠的方法可重新同步。 廣告管理和視訊分析的串流播放進度追蹤必須使用實際播放時間，因此報告和使用者介面行為可能無法準確追蹤媒體和廣告內容。

   * 來自此平台TVSDK之所有HTTP要求的傳入使用者代理程式取決於裝置以及該裝置上執行的iOS版本。

      使用者代理字串的值預設為作業系統指派的內容。

## 最佳實務 {#section_tvsdk_best_practices}

以下是TVSDK的建議作法：

* 針對程式內容使用HLS 3.0版或更新版本。

* 使用Apple的mediastreamvalidator工具來驗證VOD資料流。

* PTSDKConfig類別提供在向Primetime廣告決策、DRM和Video Analytics伺服器提出的請求上強制SSL的方法。

如需詳細資訊，請參閱此類別中的forceHTTPS和isForcingHTTPS方法。

>[!IMPORTANT]
>
>對第三方網域（例如廣告追蹤畫素、內容和廣告URL）的要求以及類似要求不會修改。 內容提供者和廣告伺服器應負責提供透過HTTPS支援的URL。
