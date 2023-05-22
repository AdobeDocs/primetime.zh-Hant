---
description: 可以設定隱藏字幕文本的格式，如字型、大小、顏色、邊緣和不透明度。
title: 設定隱藏標題樣式
exl-id: 7ece68ce-0dc5-4899-9834-39940bbd0332
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 設定隱藏標題樣式{#set-closed-caption-styles}

可以設定隱藏字幕文本的格式，如字型、大小、顏色、邊緣和不透明度。

1. 等待 `MediaPlayer` 至少處於PREPARED狀態。

   有關狀態的詳細資訊，請參見 [等待有效狀態](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md)。
1. 建立 `TextFormat` 實例。

   您可以立即提供所有隱藏字幕樣式參數，也可以稍後設定這些參數。

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

1. （可選）獲取當前隱藏字幕樣式設定 `MediaPlayer.ccStyle`。

   返回值是 `TextFormat` 。

   如果以前未設定樣式，它將返回TextFormat對象，該對象具有每個屬性的預設值：

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. 要更改樣式設定，請使用 `MediaPlayer.ccStyle`，傳遞實例 `TextFormat` 。

   即使當前媒體流沒有隱藏字幕，也可以使用此方法。

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >設定閉合字幕樣式是非同步的，因此更改可能需要幾秒鐘才能顯示在螢幕上。
