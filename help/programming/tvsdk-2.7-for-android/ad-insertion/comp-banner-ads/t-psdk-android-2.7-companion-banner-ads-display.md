---
description: 若要顯示橫幅廣告，您必須建立橫幅例項，並允許TVSDK接聽與廣告相關的事件。
title: 顯示橫幅廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 顯示橫幅廣告 {#display-banner-ads}

若要顯示橫幅廣告，您必須建立橫幅例項，並允許TVSDK接聽與廣告相關的事件。

TVSDK提供透過與線性廣告相關的隨附橫幅廣告清單 `AdPlaybackEventListener.onAdBreakStart` 事件。

資訊清單可透過以下方式指定隨附橫幅廣告：

* HTML片段
* iFrame頁面的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個隨附廣告，TVSDK會指出您的應用程式可用的型別。

1. 新增監聽器 `AdPlaybackEventListener.onAdBreakStart` 具有以下動作的事件：

   * 清除橫幅例項中的現有廣告。
   * 從取得隨附廣告清單 `Ad.getCompanionAssets`.
   * 如果隨附廣告清單不是空的，請反複檢視橫幅例項的清單。

     每個橫幅例項(一個 `AdAsset`)包含寬度、高度、資源型別（html、iframe或靜態）等資訊，以及顯示隨附橫幅所需的資料。
   * 如果視訊廣告沒有隨附廣告預訂，則隨附資產清單不包含該視訊廣告的資料。
   * 若要顯示獨立顯示廣告，請在指令碼中新增邏輯，以在適當的橫幅例項中執行一般DFP (DoubleClick for Publishers)顯示廣告標籤。
   * 將橫幅資訊傳送至頁面上會在適當位置顯示橫幅的函式。

     這通常是 `div`，而您的函式會使用 `div ID` 以顯示橫幅。
