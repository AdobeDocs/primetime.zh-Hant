---
description: 您可以設定隱藏式字幕文字的格式，例如字型、大小、顏色、邊緣和不透明度。
title: 設定隱藏式字幕樣式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 設定隱藏式字幕樣式{#set-closed-caption-styles}

您可以設定隱藏式字幕文字的格式，例如字型、大小、顏色、邊緣和不透明度。

1. 等待 `MediaPlayer` 至少處於「已準備」狀態。

   如需狀態的詳細資訊，請參閱 [等待有效的狀態](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. 建立 `TextFormat` 執行個體。

   您可以現在提供所有隱藏式字幕樣式引數，或稍後再設定。

   ```js
   new TextFormat( 
       font,   
       fontColor,  
       edgeColor,   
       fontEdge,  
       backgroundColor,   
       fillColor,  
       size,   
       fontOpacity,   
       backgroundOpacity,  
       fillOpacity, 
       bottomInset 
       safeArea) → {AdobePSDK.TextFormat}
   ```

1. （可選）透過取得目前的隱藏式字幕樣式設定 `MediaPlayer.ccStyle`.

   傳回值是 `TextFormat` 介面。

   如果先前未設定任何樣式，則會傳回TextFormat物件，其中包含每個屬性的預設值：

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. 若要變更樣式設定，請使用 `MediaPlayer.ccStyle`，傳遞的例項 `TextFormat` 介面。

   即使目前的媒體資料流沒有隱藏式字幕，您也可以使用此方法。

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >設定隱藏式字幕樣式為非同步，因此變更可能需要幾秒鐘才會顯示在畫面上。
