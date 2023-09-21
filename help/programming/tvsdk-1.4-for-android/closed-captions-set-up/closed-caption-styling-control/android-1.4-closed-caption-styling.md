---
description: 您可以使用TextFormat類別為隱藏式字幕軌跡提供樣式資訊。 這會設定播放器所顯示之任何隱藏式字幕的樣式。
title: 控制隱藏式字幕樣式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 控制隱藏式字幕樣式 {#control-closed-caption-styling-overview}

您可以使用TextFormat類別為隱藏式字幕軌跡提供樣式資訊。 這會設定播放器所顯示之任何隱藏式字幕的樣式。

此類別會封裝隱藏式字幕樣式資訊，例如字型型別、大小、顏色和背景不透明度。 關聯的協助程式類別， `TextFormatBuilder`，有助於使用隱藏式字幕樣式設定。

## 設定隱藏式字幕樣式 {#set-closed-caption-styles}

您可以使用TVSDK方法設定隱藏式字幕文字的樣式。

1. 等候媒體播放器至少處於「已準備」狀態。
1. 建立 `TextFormatBuilder` 執行個體。

   您可以現在提供所有隱藏式字幕樣式引數，或稍後再設定。

   TVSDK會將隱藏式字幕樣式資訊封裝在 `TextFormat` 介面。 此 `TextFormatBuilder` 類別會建立實作此介面的物件。

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

1. 若要取得實作物件的參照 `TextFormat` 介面，呼叫 `TextFormatBuilder.toTextFormat` 公用方法。

   這會傳回 `TextFormat` 可套用至媒體播放器的物件。

   ```java
   public TextFormat toTextFormat()
   ```

1. 您可以執行下列任一項動作，取得目前的隱藏式字幕樣式設定：

   * 透過取得所有樣式設定 `MediaPlayer.getCCStyle`.

     傳回值是 `TextFormat` 介面。

     ```js
     /** 
     * @return the current closed captioning style.  
     * If no style was previously set, it returns a TextFormat object 
     * with default values for each attribute. 
     * @throws IllegalStateException if media player was already released. 
     */ 
     public TextFormat getCCStyle() throws IllegalStateException;
     ```

   * 透過，一次取得一個設定 `TextFormat` 介面getter方法。

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

1. 若要變更樣式設定，請執行下列任一項動作：

   >[!NOTE]
   >
   >您無法變更WebVTT註解的大小。

   * 使用setter方法 `MediaPlayer.setCCStyle`，傳遞的例項 `TextFormat` 介面：

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

   * 使用 `TextFormatBuilder` 類別，定義個別的setter方法。

     此 `TextFormat` 介面會定義不可變物件，因此只有getter方法而沒有setter。 您只能使用設定隱藏式字幕樣式引數 `TextFormatBuilder` 類別：

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

設定隱藏式字幕樣式為非同步操作，因此變更可能需要幾秒鐘才會顯示在畫面上。

## 隱藏式字幕樣式選項 {#closed-caption-styling-options}

您可以指定數個註解樣式選項，這些選項會覆寫原始註解中的樣式選項

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
>在定義預設值的選項（例如DEFAULT）中，該值是指最初指定註解時的設定。

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
   <td colname="1"> 字型邊緣 </td> 
   <td colname="2"> <p>用於字型邊緣的效果，例如凸出或無。 </p> <p>只能設定為以下定義的值： <span class="codeph"> TextFormat.FontEdge </span> 分項清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型顏色 </td> 
   <td colname="2"> <p>字型顏色。 </p> <p>只能設定為以下定義的值： <span class="codeph"> TextFormat.Color </span> 分項清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 邊緣顏色 </td> 
   <td colname="2"> <p>邊緣效果的顏色。 </p> <p>可設定為字型顏色可用的任何值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景顏色 </td> 
   <td colname="2"> <p>背景字元儲存格顏色。 </p> <p>只能設定為可用於字型顏色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填色顏色 </td> 
   <td colname="2"> <p>文字所在視窗的背景色彩。 </p> <p>可設定為字型顏色可用的任何值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型不透明度 </td> 
   <td colname="2"> <p>文字的不透明度。 </p> <p>以從0 （完全透明）到100 （完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_不透明度 </span> 的為100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景不透明度 </td> 
   <td colname="2"> <p>背景字元儲存格的不透明度。 </p> <p>以從0 （完全透明）到100 （完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_不透明度 </span> 背景為100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填色不透明度 </td> 
   <td colname="2"> <p>註解視窗背景的不透明度。 </p> <p>以從0 （完全透明）到100 （完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_不透明度 </span> 填色為0。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 註解格式範例 {#examples-caption-formatting}

您可以指定隱藏式字幕格式。

**範例1：明確指定格式值**

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

**範例2：在引數中指定格式值**

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
