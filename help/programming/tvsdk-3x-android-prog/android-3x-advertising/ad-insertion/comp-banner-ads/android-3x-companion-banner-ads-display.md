---
description: 若要顯示橫幅廣告，您必須建立橫幅例項，並允許TVSDK監聽廣告相關事件。
seo-description: 若要顯示橫幅廣告，您必須建立橫幅例項，並允許TVSDK監聽廣告相關事件。
seo-title: 顯示橫幅廣告
title: 顯示橫幅廣告
uuid: cfd4b26c-9643-4b60-9aff-bc27dec289f1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 顯示橫幅廣告 {#display-banner-ads}

若要顯示橫幅廣告，您必須建立橫幅例項，並允許TVSDK監聽廣告相關事件。

TVSDK提供與事件中的線性廣告相關的配套橫幅廣告清 `AdPlaybackEventListener.onAdBreakStart` 單。

清單可透過下列方式指定配套橫幅廣告：

* HTML程式碼片段
* iFrame頁面的URL
* 靜態影像或Adobe Flash SWF檔案的URL

對於每個配套廣告，TVSDK會指出您的應用程式有哪些類型。

1. 為執行下列操作的 `AdPlaybackEventListener.onAdBreakStart` 事件添加偵聽程式：

   * 清除橫幅例項中的現有廣告。
   * 從中取得配套廣告清單 `Ad.getCompanionAssets`。
   * 如果配套廣告清單不是空的，請在橫幅例項清單上重複。

      每個橫幅實例( `AdAsset`an)都包含寬度、高度、資源類型（html、iframe或靜態），以及顯示配套橫幅所需的資料。
   * 如果視訊廣告沒有隨附的配套廣告，則配套資產清單中不會包含該視訊廣告的資料。
   * 若要顯示獨立顯示廣告，請將邏輯新增至指令碼，以在適當的橫幅實例中執行一般的DFP（發佈者的DoubleClick）顯示廣告標籤。
   * 將橫幅資訊傳送至頁面上顯示適當位置橫幅的函式。

      這通常是 `div`，您的函式會使 `div ID` 用來顯示橫幅。