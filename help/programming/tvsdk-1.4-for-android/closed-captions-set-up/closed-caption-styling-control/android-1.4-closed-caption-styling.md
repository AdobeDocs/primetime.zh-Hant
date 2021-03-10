---
description: 您可以使用TextFormat類別，為隱藏字幕音軌提供樣式資訊。 如此可設定播放器所顯示之隱藏字幕的樣式。
title: 控制隱藏字幕樣式
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# 控制隱藏字幕樣式{#control-closed-caption-styling-overview}

您可以使用TextFormat類別，為隱藏字幕音軌提供樣式資訊。 如此可設定播放器所顯示之隱藏字幕的樣式。

此類別封裝隱藏字幕樣式資訊，例如字型類型、大小、色彩和背景不透明度。 關聯的幫助類`TextFormatBuilder`便於使用隱藏字幕樣式設定。

## 設定隱藏字幕樣式{#set-closed-caption-styles}

您可以使用TVSDK方法來設定隱藏字幕文字的樣式。

1. 等待媒體播放器至少處於「已準備」狀態。
1. 建立`TextFormatBuilder`實例。

   您現在可以提供所有隱藏字幕樣式參數，或稍後再設定。

   TVSDK會將隱藏字幕樣式資訊封裝在`TextFormat`介面中。 `TextFormatBuilder`類建立實現此介面的對象。

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

1. 要獲取對實現`TextFormat`介面的對象的引用，請調用`TextFormatBuilder.toTextFormat`公用方法。

   這會傳回可套用至媒體播放器的`TextFormat`物件。

   ```java
   public TextFormat toTextFormat()
   ```

1. （可選）執行下列任一操作，以取得目前的隱藏字幕樣式設定：

   * 取得所有樣式設定與`MediaPlayer.getCCStyle`。

      返回值是`TextFormat`介面的實例。

      ```js
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

   * 透過`TextFormat`介面getter方法一次取得一個設定。

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

1. 要更改樣式設定，請執行下列操作之一：

   >[!NOTE]
   >
   >您無法變更WebVTT標題的大小。

   * 使用setter方法`MediaPlayer.setCCStyle` ，傳遞`TextFormat`介面的實例：

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

   * 使用`TextFormatBuilder`類別，它定義各個setter方法。

      `TextFormat`介面定義不可變對象，因此只有getter方法和無設定器。 您只能使用`TextFormatBuilder`類別來設定隱藏字幕樣式參數：

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

設定隱藏字幕樣式是非同步操作，因此變更可能需要數秒鐘才會顯示在畫面上。

## 隱藏字幕樣式選項{#closed-caption-styling-options}

您可以指定數個標題樣式選項，而這些選項會覆寫原始標題中的樣式選項

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
>在定義預設值（例如DEFAULT）的選項中，該值是指最初指定標題時的設定。

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
   <td colname="2"> <p>字型類型。 </p> <p>只能設定為由<span class="codeph"> TextFormat.Font </span>枚舉定義的值，並表示（例如，帶有或不帶有序列）。 </p> <p>提示： 裝置上的實際可用字型可能會有所不同，並會視需要使用替代。 單空間與serifs通常用作替代，儘管這種替代可以是系統特定的。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 大小 </td> 
   <td colname="2"> <p>字幕大小。 </p> <p> 只能設定為<span class="codeph"> TextFormat.Size </span>枚舉定義的值： 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 中 </span> -標準尺寸 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> LARGE  </span> -大約30%（中） </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 小 </span> 型——大約比中型小30% </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> DEFAULT  </span> -標題的預設大小；與介質相同 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型邊緣 </td> 
   <td colname="2"> <p>用於字型邊緣的效果，例如凸起或無。 </p> <p>只能設定為由<span class="codeph"> TextFormat.FontEdge </span>枚舉定義的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型顏色 </td> 
   <td colname="2"> <p>字型顏色。 </p> <p>只能設定為<span class="codeph"> TextFormat.Color </span>枚舉定義的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 邊緣顏色 </td> 
   <td colname="2"> <p>邊緣效果的顏色。 </p> <p>可以設定為任何可用於字型顏色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景顏色 </td> 
   <td colname="2"> <p>背景字元儲存格顏色。 </p> <p>只能設定為字型顏色可用的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填色顏色 </td> 
   <td colname="2"> <p>文本所在窗口的背景顏色。 </p> <p>可以設定為任何可用於字型顏色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型不透明度 </td> 
   <td colname="2"> <p>文字的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 字型的DEFAULT_ </span> OPACITY為100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景不透明度 </td> 
   <td colname="2"> <p>背景字元儲存格的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 背景的DEFAULT_ </span> OPACITY為100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填滿不透明度 </td> 
   <td colname="2"> <p>標題視窗背景的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 填色的DEFAULT_ </span> OPACITY為0。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 標題格式示例{#examples-caption-formatting}

您可以指定隱藏字幕格式。

**範例1:明確指定格式值**

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

**範例2:在參數中指定格式值**

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
