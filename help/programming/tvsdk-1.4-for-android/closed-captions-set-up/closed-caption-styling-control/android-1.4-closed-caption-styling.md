---
description: 可以使用TextFormat類為隱藏字幕軌道提供樣式資訊。 這將設定播放器顯示的任何隱藏字幕的樣式。
title: 控制隱藏字幕樣式
exl-id: 0083c141-9c03-46a2-902b-6e7eebaadea4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 控制隱藏字幕樣式 {#control-closed-caption-styling-overview}

可以使用TextFormat類為隱藏字幕軌道提供樣式資訊。 這將設定播放器顯示的任何隱藏字幕的樣式。

此類封裝了隱藏標題樣式資訊，如字型類型、大小、顏色和背景不透明度。 關聯的幫助程式類， `TextFormatBuilder`，便於使用隱藏字幕樣式設定。

## 設定隱藏標題樣式 {#set-closed-caption-styles}

可以使用TVSDK方法來設定隱藏標題文本的樣式。

1. 等待媒體播放器至少處於PREPARED狀態。
1. 建立 `TextFormatBuilder` 實例。

   您可以立即提供所有隱藏字幕樣式參數，也可以稍後設定這些參數。

   TVSDK將隱藏的字幕樣式資訊封裝到 `TextFormat` 。 的 `TextFormatBuilder` 類建立實現此介面的對象。

   ```java
   public TextFormatBuilder( 
      Font font, 
      Size size, 
      FontEdge fontEdge, 
      Color fontColor, 
      Color backgroundColor, 
      Color fillColor, 
      Color edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity)
   ```

1. 獲取對實現 `TextFormat` 介面，調用 `TextFormatBuilder.toTextFormat` 公共方法。

   這返回 `TextFormat` 可應用於媒體播放器的對象。

   ```java
   public TextFormat toTextFormat()
   ```

1. （可選）通過執行下列操作之一獲取當前隱藏字幕樣式設定：

   * 獲取所有樣式設定 `MediaPlayer.getCCStyle`。

      返回值是 `TextFormat` 。

      ```js
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

   * 通過 `TextFormat` 介面getter方法。

      ```js
      public Color getFontColor(); 
      public Color getBackgroundColor(); 
      public Color getFillColor(); // retrieve the font fill color 
      public Color getEdgeColor(); // retrieve the font edge color 
      public Size getSize(); // retrieve the font size 
      public FontEdge getFontEdge(); // retrieve the font edge type 
      public Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity();
      ```

1. 要更改樣式設定，請執行以下操作之一：

   >[!NOTE]
   >
   >不能更改WebVTT字幕的大小。

   * 使用setter方法 `MediaPlayer.setCCStyle`，傳遞實例 `TextFormat` 介面：

      ```js
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws IllegalStateException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws IllegalStateException;
      ```

   * 使用 `TextFormatBuilder` 類，它定義單個setter方法。

      的 `TextFormat` 介面定義不可變的對象，因此只有getter方法和沒有setter。 您只能使用 `TextFormatBuilder` 類：

      ```js
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(Color backgroundColor) 
      public void setFillColor(Color fillColor) 
      // set the font-edge color 
      public void setEdgeColor(Color edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(Color fontColor)
      ```

設定隱藏字幕樣式是一個非同步操作，因此可能需要幾秒鐘才能在螢幕上顯示更改。

## 隱藏字幕樣式選項 {#closed-caption-styling-options}

可以指定多個字幕樣式選項，這些選項會覆蓋原始字幕中的樣式選項

```
public TextFormatBuilder(
 Font font,
 Size size,
 FontEdge fontEdge,
 Color fontColor,
 Color backgroundColor,
 Color fillColor,
 Color edgeColor,
 int fontOpacity,
 int backgroundOpacity,
 int fillOpacity,
 String bottomInset)
```

>[!TIP]
>
>在定義預設值（例如，DEFAULT）的選項中，該值指最初指定標題時的設定。

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> 格式 </b></th> 
   <th colname="2" class="entry"> <b>說明</b> </th> 
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
   <td colname="1"> 字型邊緣 </td> 
   <td colname="2"> <p>用於字型邊緣的效果，如凸起或無。 </p> <p>只能設定為由 <span class="codeph"> 文本格式。字型邊緣 </span> 枚舉。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型顏色 </td> 
   <td colname="2"> <p>字型顏色。 </p> <p>只能設定為由 <span class="codeph"> 文本格式。顏色 </span> 枚舉。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 邊緣顏色 </td> 
   <td colname="2"> <p>邊緣效果的顏色。 </p> <p>可以設定為字型顏色可用的任何值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景顏色 </td> 
   <td colname="2"> <p>背景字元單元格顏色。 </p> <p>只能設定為字型顏色可用的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填充顏色 </td> 
   <td colname="2"> <p>文本所在窗口的背景顏色。 </p> <p>可以設定為字型顏色可用的任何值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型不透明度 </td> 
   <td colname="2"> <p>文本的不透明度。 </p> <p>表示為0（完全透明）到100（完全不透明）的百分比。 <span class="codeph"> 預設不透明度 </span> 字型為100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景不透明度 </td> 
   <td colname="2"> <p>背景字元單元格的不透明度。 </p> <p>表示為0（完全透明）到100（完全不透明）的百分比。 <span class="codeph"> 預設不透明度 </span> 背景是100 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填充不透明度 </td> 
   <td colname="2"> <p>字幕窗口背景的不透明度。 </p> <p>表示為0（完全透明）到100（完全不透明）的百分比。 <span class="codeph"> 預設不透明度 </span> 填充為0。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 標題格式示例 {#examples-caption-formatting}

可以指定隱藏字幕格式。

**示例1:顯式指定格式值**

```java
private final MediaPlayer.PlaybackEventListener  
  _playbackEventListener = new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder(TextFormat.Font.DEFAULT, 
        TextFormat.Size.DEFAULT, 
        TextFormat.FontEdge.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY).toTextFormat(); 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 
```

**示例2:在參數中指定格式值**

```java
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param size 
* The desired text size. 
* @param fontEdge 
* The desired font edge. 
* @param fontColor 
* The desired font color. 
* @param backgroundColor 
* The desired background color. 
* @param fillColor 
* The desired fill color. 
* @param edgeColor 
* The desired color to draw the text edges. 
* @param fontOpacity  
* The desired font opacity. 
* @param backgroundOpacity 
* The desired background opacity. 
* @param fillOpacity 
* The desired fill opacity.  
*/ 
public TextFormatBuilder( 
    Font font, Size size, FontEdge fontEdge, 
    Color fontColor, Color backgroundColor,  
    Color fillColor, Color edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat toTextFormat(); 
 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public TextFormatBuilder setFont(Font font); 
... 
```
