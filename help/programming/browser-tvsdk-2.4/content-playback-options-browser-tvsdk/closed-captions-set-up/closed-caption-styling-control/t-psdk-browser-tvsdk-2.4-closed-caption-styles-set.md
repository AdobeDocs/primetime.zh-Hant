---
description: 您可以設定隱藏字幕文字的格式，例如字型、大小、顏色、邊緣和不透明度。
title: 設定隱藏字幕樣式
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 設定隱藏字幕樣式{#set-closed-caption-styles}

您可以設定隱藏字幕文字的格式，例如字型、大小、顏色、邊緣和不透明度。

1. 等待`MediaPlayer`至少處於「已準備」狀態。

   有關狀態的詳細資訊，請參閱[等待有效狀態](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md)。
1. 建立`TextFormat`實例。

   您現在可以提供所有隱藏字幕樣式參數，或稍後再設定。

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

1. （可選）取得目前包含`MediaPlayer.ccStyle`的隱藏字幕樣式設定。

   返回值是`TextFormat`介面的實例。

   如果先前未設定樣式，則會傳回TextFormat物件，其中包含每個屬性的預設值：

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. 要更改樣式設定，請使用`MediaPlayer.ccStyle` ，傳遞`TextFormat`介面的實例。

   即使目前的媒體串流沒有隱藏字幕，您仍可使用此方法。

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >設定隱藏字幕樣式是非同步的，因此變更可能需要幾秒鐘的時間才會出現在螢幕上。

