---
description: 若要最有效率地使用TVSDK，您應考慮其運作的特定詳細資訊，並遵循特定最佳實務。
seo-description: 若要最有效率地使用TVSDK，您應考慮其運作的特定詳細資訊，並遵循特定最佳實務。
seo-title: 考量事項和最佳實務
title: 考量事項和最佳實務
uuid: a65c9739-ed83-4519-8ae5-7ba4c8f1ca49
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 考量事項和最佳實務 {#considerations-and-best-practices}

若要最有效率地使用TVSDK，您應考慮其運作的特定詳細資訊，並遵循特定最佳實務。

## 考量事項 {#section_tvsdk_considerations}

使用TVSDK時，請記住下列資訊：

* Adobe Primetime無法在iOS模擬器上運作。

   您必須使用真正的裝置進行測試。

* 僅HTTP即時串流(HLS)內容支援播放。

* 主視訊內容可以多路復用，其中視訊和音訊串流位於相同的轉譯中，或非多路復用，其中視訊和音訊串流位於不同的轉譯中。

* TVSDK API是在Objective-C中實作。

* 視訊播放需要原生的Apple AV Foundation架構。 這會影響媒體資源（包括隱藏字幕和時間軸）的存取方式與時間：

   * 時間軸調整無法在初始設定後修訂。

      例如，廣告播放後，無法從時間軸移除。 如果使用者在簡報中尋找回來，即使原則是移除廣告，也會重播相同的廣告。

   * 根據編碼器精度，實際編碼媒體持續時間可能與串流資源清單中記錄的持續時間不同。

      在理想的虛擬時間軸和實際播放時間軸之間沒有可靠的重新同步方法。 廣告管理和視訊分析的串流播放進度追蹤必須使用實際播放時間，因此報告和使用者介面行為可能無法精確追蹤媒體和廣告內容。

   * 此平台上來自TVSDK的所有HTTP要求的傳入使用者代理由裝置上執行的iOS版本所決定。

      使用者代理字串的值預設為作業系統指派的值。

## 最佳實務 {#section_tvsdk_best_practices}

以下是TVSDK的建議實務：

* 使用HLS 3.0版或更新版本來取得程式內容。

* 使用Apple的mediastreamvalidator工具來驗證VOD串流。

* PTSDKConfig類別提供對Primetime廣告決策、DRM和視訊分析伺服器提出的要求強制執行SSL的方法。

如需詳細資訊，請參閱此類別中的forceHTTPS和isForcingHTTPS方法。

[!IMPORTANT]

不會修改對第三方網域（例如廣告追蹤像素、內容和廣告URL）的請求，以及類似的請求。 內容提供者和廣告伺服器有責任提供透過HTTPS支援的URL。