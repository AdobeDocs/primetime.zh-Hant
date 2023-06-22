---
title: 功能管理員
description: 功能管理員可讓您控制個別功能，而不需遍歷整個TVSDK來搜尋可能分散在多個位置的一個功能的程式碼。
exl-id: dbf2dc8b-6067-4d94-9c3c-553452b7ffd9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 功能管理員 {#feature-managers}

功能管理員可讓您控制個別功能，而不需遍歷整個TVSDK來搜尋可能分散在多個位置的一個功能的程式碼。 功能管理員會將程式碼壓縮成每個功能的一個類別。 功能管理員會等待TVSDK事件的觸發程式，然後通知使用功能管理員處理結果的類別。 功能管理員會為類別提供必要資訊。

功能管理員會執行下列工作：

* **觸發TVSDK功能。**
這些是觸發TVSDK功能的函式呼叫。 例如， 
`PlaybackManager.play()` 當播放器應用程式需要啟動視訊播放時，就會呼叫。

* **接聽TVSDK事件。**
功能管理員需要監聽TVSDK事件，才能從TVSDK取得資訊。 例如， 
`AdsManager` 偵聽TVSDK廣告事件，以在廣告插播開始時收到通知。

* **將事件分派給處理常式。**
功能管理員收到並處理來自TVSDK的事件後，會通知使用者端處理該事件。 例如，在 
`AdsManager` 會收到廣告插播開始事件，並告訴播放器片段在UI中反映此變更（停用推移列、顯示廣告覆蓋圖等）。

Primetime參照實施包括下列功能管理員：

| 功能管理員 | 預設檔案 | 功能 |  |
|---|---|---|---|
| 視訊播放 | Playbackmanager | HLS播放與控制、DVR播放與控制、緩衝區控制以及多位元速率處理。 | 必填 |
| DRM內容保護 | DrmManager | 內容保護。 | 必填 |
| 廣告插入 | AdsManager | 廣告插入，包括Adobe Primetime ad decisioning直接廣告插播和自訂廣告插播。 | 可選 |
| 隱藏式字幕 | CCManager | 隱藏式字幕和VTT字幕。 | 可選 |
| 延遲繫結音訊 | AAManager | 延遲繫結音訊。 | 可選 |
| QoS | QosManager | QoS統計資料。 | 可選 |
| 權利 | EntitlementManager | Primetime驗證許可權整合。 | 可選 |

參考實作包含上列的基本預設類別，以及尾碼為On的對應類別。 預設類別會提供預設的TVSDK行為，而具有On尾碼的類別則包含觸發TVSDK功能及監聽該功能的TVSDK事件所需的所有程式碼。

* 對於可選功能，預設程式碼的操作方式與功能關閉時相同。
* 具有On字尾的類別會像開啟特徵一樣運作。
