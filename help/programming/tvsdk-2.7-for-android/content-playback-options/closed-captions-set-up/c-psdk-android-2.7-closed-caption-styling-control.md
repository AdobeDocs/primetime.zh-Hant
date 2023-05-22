---
description: 可以使用TextFormat類為隱藏字幕軌道提供樣式資訊，該類設定播放器顯示的隱藏字幕的樣式。
title: 控制隱藏字幕樣式
exl-id: fa96f9f5-f709-4749-90c8-cf237cf074c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 控制隱藏字幕樣式 {#control-closed-caption-styling}

可以使用TextFormat類為隱藏字幕軌道提供樣式資訊，該類設定播放器顯示的隱藏字幕的樣式。

此類封裝隱藏的標題樣式資訊，如字型類型、大小、顏色和背景不透明度。

## 設定隱藏標題樣式 {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

可以使用TVSDK方法來設定隱藏標題文本的樣式。

1. 等待媒體播放器至少位於 `PREPARED` 狀態。
1. 建立 `TextFormatBuilder` 實例。

   您可以立即提供所有隱藏字幕樣式參數，也可以稍後設定這些參數。

   TVSDK將隱藏的字幕樣式資訊封裝到 `TextFormat` 。 的 `TextFormatBuilder` 類建立實現此介面的對象。

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

1. 獲取對實現 `TextFormat` 介面，調用 `TextFormatBuilder.toTextFormat` 公共方法。

   >[!NOTE]
   >
   >這返回 `TextFormat` 可應用於媒體播放器的對象。

   ```java
   public TextFormat toTextFormat()
   ```

1. （可選）通過執行下列操作之一獲取當前隱藏字幕樣式設定：

   * 獲取所有樣式設定 `MediaPlayer.getCCStyle` 返回值是 `TextFormat` 。

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * 通過 `TextFormat` 介面getter方法。

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

1. 要更改樣式設定，請執行以下操作之一：

   * 使用setter方法 `MediaPlayer.setCCStyle`，傳遞實例 `TextFormat` 介面：

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

   * 使用 `TextFormatBuilder` 類，它定義單個setter方法。

      的 `TextFormat` 介面定義不可變的對象，因此只有getter方法和沒有setter。 您只能使用 `TextFormatBuilder` 類：

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
      >**顏色設定：** 在Android TVSDK 2.X中，對隱藏字幕的顏色樣式進行了增強。 該增強允許使用表示RGB顏色值的十六進位字串設定隱藏字幕顏色。 RGB十六進位顏色表示法是您在應用程式(如Photoshop:
      >
      >* FFFFFF =黑色
      >* 000000 =白色
      >* FF0000 =紅色
      >* 00FF00 =綠色
      >* 000FF =藍色

      >
      >等等。
      >
      >在應用程式中，無論何時將顏色樣式資訊傳遞給 `TextFormatBuilder`，您仍然使用 `Color` 枚舉，但現在必須添加 `getValue()` 到顏色以獲取字串形式的值。 例如：
      >
      >
      ```
      >tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      >```

設定隱藏字幕樣式是一個非同步操作，因此可能需要幾秒鐘才能在螢幕上顯示更改。

## 隱藏字幕樣式選項 {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

您可以指定多個字幕樣式選項，這些選項會覆蓋原始字幕中的樣式選項。

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
  <tr rowsep="1"> 
   <td colname="1"> 底部插入 </td> 
   <td colname="2"> <p>從字幕窗口底部垂直距離可避免字幕。 </p> <p>表示為字幕窗口高度的百分比（例如「20%」）或像素數（例如「20」）。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 安全區 </td> 
   <td colname="2"> <p>螢幕邊緣周圍0%到25%之間不顯示字幕的區域。 </p> <p>預設情況下，WebVTT的安全區域為0%。 此設定允許應用程式覆蓋該預設值。 如果提供兩個值，例如字串"10%,20%"，則第一個值是水準安全區，第二個值是垂直安全區。 如果提供一個值，例如字串"15%"，則垂直軸和水準軸都使用指定的安全區域。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 標題格式示例 {#section_58E8E82494EC4683B010FFDE67485CF9}

下面是一些示例，向您顯示如何指定隱藏的標題格式。

**示例1:顯式指定格式值**

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
