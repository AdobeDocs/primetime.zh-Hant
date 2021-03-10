---
title: 功能管理員
description: 功能管理員可讓您控制個別功能，而不需遍歷整個TVSDK，以搜尋可分散在多個位置的功能的程式碼。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---


# 功能管理器{#feature-managers}

功能管理員可讓您控制個別功能，而不需遍歷整個TVSDK，以搜尋可分散在多個位置的功能的程式碼。 功能管理員將程式碼簡化為每個功能的一個類別。 功能管理員會等待TVSDK事件的觸發器，然後通知使用功能管理員來處理結果的類別。 功能管理員會為類別提供所需資訊。

功能管理員會執行下列工作：

* **觸發TVSDK功能。**
這些是觸發TVSDK功能的函式呼叫。例如， 
`PlaybackManager.play()` 在播放器應用程式需要啟動視訊播放時呼叫。

* **監聽TVSDK事件。**
功能管理員需要監聽TVSDK事件，才能從TVSDK取得資訊。例如， 
`AdsManager` 監聽TVSDK廣告事件，以便在廣告中斷開始時收到通知。

* **將事件調度到處理程式。**
功能管理員從TVSDK接收並處理事件後，會通知用戶端處理該事件。例如，在 
`AdsManager` 收到廣告插播開始事件時，會告訴播放器片段在UI中反映此變更（停用拖曳列、顯示廣告覆蓋等）。

Primetime參考實作包含下列功能管理員：

| 功能管理員 | 預設檔案 | 功能 |  |
|---|---|---|---|
| 視訊播放 | PlaybackManager | HLS播放與控制、DVR播放與控制、緩衝控制和多位元速率處理。 | 必要 |
| DRM內容保護 | DrmManager | 內容保護。 | 必要 |
| 廣告插入 | AdsManager | 廣告插入，包括Adobe Primetime廣告決策直接廣告插播和自訂廣告插播。 | 可選 |
| 隱藏字幕 | CCManager | 隱藏字幕和VTT字幕。 | 可選 |
| 延遲裝訂音訊 | AAManager | 延遲裝訂音訊。 | 可選 |
| QoS | QosManager | QoS統計資訊。 | 可選 |
| 權益 | EntitlementManager | Primetime驗證權益整合。 | 可選 |

參考實現包含上列的基本預設類和尾碼為On的對應類。 預設類別提供預設的TVSDK行為，而尾碼為「開啟」的類別則包含觸發TVSDK功能並監聽該功能之TVSDK事件所需的所有程式碼。

* 對於可選功能，預設代碼的操作方式與關閉功能的方式相同。
* 具有「開啟」字尾的類會像開啟功能一樣運作。