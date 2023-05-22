---
description: 您可以指定多個字幕樣式選項，這些選項會覆蓋原始字幕中的樣式選項。
title: 隱藏字幕樣式選項
exl-id: df5377c2-741b-4239-b345-145753896c6b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 隱藏字幕樣式選項{#closed-caption-styling-options}

您可以指定多個字幕樣式選項，這些選項會覆蓋原始字幕中的樣式選項。

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
>在定義預設值的選項中(例如， `DEFAULT`)，該值指最初指定標題時的設定。

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
   <td colname="2"> <p>字型類型。 </p> <p>只能設定為由 <span class="codeph"> TextFormat.Font </span> 枚舉和表示，例如，帶有或不帶serif的單間距。 </p> <p>提示：設備上可用的實際字型可能會有所不同，必要時會使用替代。 帶有序列的單空間通常用作替代，儘管此替代可以是系統特定的。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 大小 </td> 
   <td colname="2"> <p>標題的大小。 </p> <p> 只能設定為由 <span class="codeph"> TextFormat.Size </span> 枚舉： 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 中 </span>  — 標準大小 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 大 </span>  — 比中大約30% </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 小 </span>  — 比中小約30% </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> 預設 </span>  — 標題的預設大小；與介質相同 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型顏色 </td> 
   <td colname="2"> <p>字型顏色。 </p> <p>只能設定為由 <span class="codeph"> 文本格式。顏色 </span> 枚舉。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景顏色 </td> 
   <td colname="2"> <p>背景字元單元格顏色。 </p> <p>只能設定為字型顏色可用的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型不透明度 </td> 
   <td colname="2"> <p>文本的不透明度。 </p> <p>表示為0（完全透明）到100（完全不透明）的百分比。 <span class="codeph"> 預設不透明度 </span> 字型為100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 底部內置 </td> 
   <td colname="2"> <p>從字幕窗口底部垂直距離可避免字幕。 </p> <p>表示為字幕窗口高度的百分比（例如「20%」）或像素數（例如「20」）。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 安全區 </td> 
   <td colname="2"> <p>螢幕邊緣周圍0%到25%之間不顯示字幕的區域。 </p> <p>預設情況下，608/708的安全區為12%,WebVTT的安全區為0%。 此設定允許應用程式覆蓋該預設值。 如果提供兩個值，例如字串"10%,20%"，則第一個值是水準安全區，第二個值是垂直安全區。 如果提供一個值，例如字串"15%"，則垂直軸和水準軸都使用指定的安全區域。 </p> </td> 
  </tr> 
 </tbody> 
</table>
