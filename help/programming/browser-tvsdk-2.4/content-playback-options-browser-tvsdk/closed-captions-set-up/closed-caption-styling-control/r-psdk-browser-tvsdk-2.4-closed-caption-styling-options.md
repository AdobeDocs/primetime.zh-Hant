---
description: 您可以指定數個註解樣式選項，這些選項會覆寫原始註解中的樣式選項。
title: 隱藏式字幕樣式選項
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 隱藏式字幕樣式選項{#closed-caption-styling-options}

您可以指定數個註解樣式選項，這些選項會覆寫原始註解中的樣式選項。

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
   bottomInset, 
   safeArea) 
```

>[!TIP]
>
>在定義預設值的選項中(例如 `DEFAULT`)，該值代表最初指定註解時的設定。

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 格式 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 字型 </td> 
   <td colname="2"> <p>字型型別。 </p> <p>只能設定為以下定義的值： <span class="codeph"> TextFormat.Font </span> 分項清單，並代表（例如，有或沒有襯線）等寬。 </p> <p>提示：裝置上可用的實際字型可能會有所不同，並會視需要使用替代。 通常使用含襯線的等寬做為替代字元，不過此替代字元可能是系統專屬的。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 大小 </td> 
   <td colname="2"> <p>註解的大小。 </p> <p> 只能設定為以下定義的值： <span class="codeph"> TextFormat.Size </span> 分項清單： 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 中 </span>  — 標準大小 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 大 </span>  — 大約比中號大30% </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 小 </span>  — 大約比中型小30% </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> 預設 </span>  — 註解的預設大小；與「中」相同 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型顏色 </td> 
   <td colname="2"> <p>字型顏色。 </p> <p>只能設定為以下定義的值： <span class="codeph"> TextFormat.Color </span> 分項清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景顏色 </td> 
   <td colname="2"> <p>背景字元儲存格顏色。 </p> <p>只能設定為可用於字型顏色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型不透明度 </td> 
   <td colname="2"> <p>文字的不透明度。 </p> <p>以從0 （完全透明）到100 （完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_不透明度 </span> 的為100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 底部內縮 </td> 
   <td colname="2"> <p>要避免的註解與註解視窗底部的垂直距離。 </p> <p>以註解視窗高度的百分比（例如「20%」）或畫素數（例如「20」）表示。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 安全區域 </td> 
   <td colname="2"> <p>熒幕邊緣的區域，介於0%到25%之間，不會顯示註解。 </p> <p>根據預設，608/708的安全區域是12%，WebVTT的安全區域是0%。 此設定可讓您的應用程式覆寫該預設值。 如果提供兩個值，例如，字串「10%，20%」，則第一個值為水準安全區域，第二個值為垂直安全區域。 如果提供一個值（例如，字串「15%」），則垂直軸和水平軸都會使用指定的安全區域。 </p> </td> 
  </tr> 
 </tbody> 
</table>
