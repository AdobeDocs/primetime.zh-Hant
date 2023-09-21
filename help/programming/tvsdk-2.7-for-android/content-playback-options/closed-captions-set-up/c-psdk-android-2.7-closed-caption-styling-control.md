---
description: 您可以使用TextFormat類別為隱藏式字幕軌跡提供樣式資訊，該類別會設定播放器顯示的隱藏式字幕樣式。
title: 控制隱藏式字幕樣式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 控制隱藏式字幕樣式 {#control-closed-caption-styling}

您可以使用TextFormat類別為隱藏式字幕軌跡提供樣式資訊，該類別會設定播放器顯示的隱藏式字幕樣式。

此類別會封裝隱藏式字幕樣式資訊，例如字型型別、大小、顏色和背景不透明度。

## 設定隱藏式字幕樣式 {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

您可以使用TVSDK方法設定隱藏式字幕文字的樣式。

1. 等候媒體播放器至少在 `PREPARED` 狀態。
1. 建立 `TextFormatBuilder` 執行個體。

   您可以現在提供所有隱藏式字幕樣式引數，或稍後再設定。

   TVSDK會將隱藏式字幕樣式資訊封裝在 `TextFormat` 介面。 此 `TextFormatBuilder` 類別會建立實作此介面的物件。

   ```java
   public TextFormatBuilder( 
      TextFormat.Font font, 
      TextFormat.Size size, 
      TextFormat.FontEdge fontEdge, 
      java.lang.String fontColor, 
      java.lang.String backgroundColor, 
      java.lang.String fillColor, 
      java.lang.String edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity 
      java.lang.String bottomInset, 
      java.lang.String safeArea)
   ```

1. 若要取得實作物件的參照 `TextFormat` 介面，呼叫 `TextFormatBuilder.toTextFormat` 公用方法。

   >[!NOTE]
   >
   >這會傳回 `TextFormat` 可套用至媒體播放器的物件。

   ```java
   public TextFormat toTextFormat()
   ```

1. 您可以執行下列任一項動作，取得目前的隱藏式字幕樣式設定：

   * 透過取得所有樣式設定 `MediaPlayer.getCCStyle` 傳回值是 `TextFormat` 介面。

     ```java
     /** 
     * @return the current closed captioning style.  
     * If no style was previously set, it returns a TextFormat object 
     * with default values for each attribute. 
     * @throws MediaPlayerException if media player was already released. 
     */ 
     public TextFormat getCCStyle() throws MediaPlayerException;
     ```

   * 透過，一次取得一個設定 `TextFormat` 介面getter方法。

     ```java
     public java.lang.String getFontColor(); 
     public java.lang.String getBackgroundColor(); 
     public java.lang.String getFillColor(); // retrieve the font fill color 
     public java.lang.String getEdgeColor(); // retrieve the font edge color 
     public TextFormat.Size getSize(); // retrieve the font size 
     public TextFormat.FontEdge getFontEdge(); // retrieve the font edge type 
     public TextFormat.Font getFont(); // retrieve the font type 
     public int getFontOpacity(); 
     public int getBackgroundOpacity(); 
     public java.lang.String getBottomInset(java.lang.String bi); 
     public java.lang.String getSafeArea(java.lang.String sa);
     ```

1. 若要變更樣式設定，請執行下列任一項動作：

   * 使用setter方法 `MediaPlayer.setCCStyle`，傳遞的例項 `TextFormat` 介面：

     ```java
     /** 
     * Sets the closed captioning style. Used to control the closed captioning font, 
     * size, color, edge and opacity.  
     * 
     * This method is safe to use even if the current media stream doesn't have closed 
     * captions. 
     * 
     * @param textFormat 
     * @throws MediaPlayerException 
     */ 
     public void setCCStyle(TextFormat textFormat) throws MediaPlayerException;
     ```

   * 使用 `TextFormatBuilder` 類別，定義個別的setter方法。

     此 `TextFormat` 介面會定義不可變物件，因此只有getter方法而沒有setter。 您只能使用設定隱藏式字幕樣式引數 `TextFormatBuilder` 類別：

     ```java
     // set font type 
     public void setFont(Font font)  
     public void setBackgroundColor(String backgroundColor) 
     public void setFillColor(String fillColor) 
     // set the font-edge color 
     public void setEdgeColor(String edgeColor)  
     // set the font size 
     public void setSize(Size size)  
     // set the font edge type 
     public void setFontEdge(FontEdge fontEdge)  
     public void setFontOpacity(int fontOpacity) 
     public void setBackgroundOpacity(int backgroundOpacity) 
     // set the font-fill opacity level 
     public void setFillOpacity(int fillOpacity)  
     public void setFontColor(String fontColor) 
     public void setBottomInset(String bi) 
     public void setSafeArea(String sa) 
     public void setTreatSpaceAsAlphaNum(bool)
     ```

     >[!IMPORTANT]
     >
     >**色彩設定：** 在Android TVSDK 2.X中，已改良隱藏式字幕的色彩樣式。 增強功能允許使用代表RGB顏色值的十六進位字串來設定隱藏式字幕顏色。 RGB十六進位色彩表示是您在Photoshop等應用程式中所使用的6位元組字串：
     >
     >* FFFFFF =黑色
     >* 000000 =白色
     >* FF0000 =紅色
     >* 00FF00 =綠色
     >* 0000FF =藍色
     >
     >等等。
     >
     >在您的應用程式中，每當您傳遞顏色樣式資訊至 `TextFormatBuilder`，您仍可使用 `Color` 分項清單和以前一樣，但現在您必須新增 `getValue()` 變更為顏色，以取得字串形式的值。 例如：
     >
     >```
     >tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
     >```
     >

設定隱藏式字幕樣式為非同步操作，因此變更可能需要幾秒鐘才會顯示在畫面上。

## 隱藏式字幕樣式選項 {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

您可以指定數個註解樣式選項，這些選項會覆寫原始註解中的樣式選項。

```java
public TextFormatBuilder( 
   Font font, 
   Size size, 
   FontEdge fontEdge, 
   String fontColor, 
   String backgroundColor, 
   String fillColor, 
   String edgeColor, 
   int fontOpacity, 
   int backgroundOpacity, 
   int fillOpacity,  
   String bottomInset 
   String safeArea)
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
  <tr rowsep="1"> 
   <td colname="1"> 下內縮 </td> 
   <td colname="2"> <p>要避免的註解與註解視窗底部的垂直距離。 </p> <p>以註解視窗高度的百分比（例如「20%」）或畫素數（例如「20」）表示。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 安全區域 </td> 
   <td colname="2"> <p>熒幕邊緣的區域，介於0%到25%之間，不會顯示註解。 </p> <p>依預設，WebVTT的安全區域是0%。 此設定可讓您的應用程式覆寫該預設值。 如果提供兩個值，例如，字串「10%，20%」，則第一個值為水準安全區域，第二個值為垂直安全區域。 如果提供一個值（例如，字串「15%」），則垂直軸和水平軸都會使用指定的安全區域。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 註解格式範例 {#section_58E8E82494EC4683B010FFDE67485CF9}

以下範例說明如何指定隱藏式字幕格式。

**範例1：明確指定格式值**

```java
private final MediaPlayer.PlaybackEventListener _playbackEventListener = 
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder( 
            TextFormat.Font.DEFAULT, 
            TextFormat.Size.DEFAULT, 
            TextFormat.FontEdge.DEFAULT, 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
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
public  
<b>TextFormatBuilder</b>( 
    Font font, Size size, FontEdge fontEdge, 
    String fontColor, String backgroundColor,  
    String fillColor, String edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat  
<b>toTextFormat</b>(); 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public  
<b>TextFormatBuilder</b> setFont(Font font); 
...
```
