---
description: 您可以指定數個標題樣式選項，而這些選項會覆寫原始標題中的樣式選項。
seo-description: 您可以指定數個標題樣式選項，而這些選項會覆寫原始標題中的樣式選項。
seo-title: 隱藏字幕樣式選項
title: 隱藏字幕樣式選項
uuid: 0e2fd9f3-e569-4b5d-9b78-86f8ee6230ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 隱藏字幕樣式選項{#closed-caption-styling-options}

您可以指定數個標題樣式選項，而這些選項會覆寫原始標題中的樣式選項。

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
>在定義預設值(例如 `DEFAULT`)的選項中，該值是指最初指定標題時的設定。

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
   <td colname="2"> <p>字型類型。 </p> <p>只能設定為由 <span class="codeph"> TextFormat.Font枚舉定義的值，並表示(例如，有序列或無序列 </span> )的單間距。 </p> <p>提示： 裝置上的實際可用字型可能會有所不同，並會視需要使用替代。 帶有序列的單空間通常用作替代，儘管這種替代可以是系統特定的。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 大小 </td> 
   <td colname="2"> <p>字幕大小。 </p> <p> 只能設定為由TextFormat.Size枚舉定義的 <span class="codeph"> 值 </span> : 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 中 </span> -標準尺寸 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 大 </span> 型——大約30% </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 小 </span> 型——大約比中型小30% </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> DEFAULT </span> -標題的預設大小；與介質相同 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型顏色 </td> 
   <td colname="2"> <p>字型顏色。 </p> <p>只能設定為由TextFormat.Color枚舉定 <span class="codeph"> 義的 </span> 值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景顏色 </td> 
   <td colname="2"> <p>背景字元儲存格顏色。 </p> <p>只能設定為字型顏色可用的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型不透明度 </td> 
   <td colname="2"> <p>文字的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 字型的 </span> DEFAULT_OPACITY為100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 底端內嵌 </td> 
   <td colname="2"> <p>從標題視窗底部的垂直距離，以避免標題。 </p> <p>以字幕視窗高度（例如"20%"）或像素數（例如"20"）的百分比表示。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 安全區 </td> 
   <td colname="2"> <p>畫面邊緣的區域介於0%到25%之間，標題不會出現。 </p> <p>依預設，608/708的安全區為12%，而WebVTT的安全區為0%。 此設定可讓您的應用程式覆寫該預設值。 如果提供兩個值，例如字串"10%,20%"，則第一個值是水準安全區，第二個值是垂直安全區。 如果提供一個值，例如字串"15%"，垂直軸和水準軸都使用指定的安全區域。 </p> </td> 
  </tr> 
 </tbody> 
</table>

