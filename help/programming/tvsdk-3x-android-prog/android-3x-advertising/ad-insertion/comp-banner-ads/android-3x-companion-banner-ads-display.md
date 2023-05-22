---
description: 要顯示橫幅廣告，您需要建立橫幅實例並允許TVSDK偵聽與廣告相關的事件。
title: 顯示橫幅廣告
exl-id: 3ccf6525-ffc1-4f45-a662-8b53cab0f448
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 顯示橫幅廣告 {#display-banner-ads}

要顯示橫幅廣告，您需要建立橫幅實例並允許TVSDK偵聽與廣告相關的事件。

TVSDK提供與通過以下連結的線性廣告關聯的夥伴橫幅廣告的清單： `AdPlaybackEventListener.onAdBreakStart` 的子菜單。

清單可通過以下方式指定伴隨橫幅廣告：

* HTML段
* iFrame頁的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個伴侶廣告，TVSDK會指示哪些類型可用於應用程式。

1. 為 `AdPlaybackEventListener.onAdBreakStart` 執行以下操作的事件：

   * 清除標題實例中的現有廣告。
   * 獲取來自的伴侶廣告清單 `Ad.getCompanionAssets`。
   * 如果伴生廣告清單不為空，則在標題實例的清單上迭代。

      每個標題實例( `AdAsset`)包含寬度、高度、資源類型（html、iframe或static）等資訊，以及顯示伴隨橫幅所需的資料。
   * 如果視頻廣告沒有隨其預訂的伴侶廣告，則伴侶資產清單中不包含該視頻廣告的資料。
   * 要顯示獨立顯示廣告，請將邏輯添加到指令碼中，以在相應的標題實例中運行正常的DFP（發佈伺服器的按兩下）顯示廣告標籤。
   * 將橫幅資訊發送到頁面上在適當位置顯示橫幅的功能。

      這通常是 `div`，您的函式使用 `div ID` 來顯示標題。
