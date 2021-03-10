---
description: 您可以使用TextFormat類別來提供隱藏字幕音軌的樣式資訊，此類別會設定播放器所顯示隱藏字幕的樣式。
title: 控制隱藏字幕樣式
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# 控制隱藏字幕樣式{#control-closed-caption-styling}

您可以使用TextFormat類別來提供隱藏字幕音軌的樣式資訊，此類別會設定播放器所顯示隱藏字幕的樣式。

此類別封裝隱藏字幕樣式資訊，例如字型類型、大小、色彩和背景不透明度。

## 設定隱藏字幕樣式{#section_C9B5E75C70DD42E59DC4DD0F308C8216}

您可以使用TVSDK方法來設定隱藏字幕文字的樣式。

1. 等待媒體播放器至少處於`PREPARED`狀態。
1. 建立`TextFormatBuilder`實例。

   您現在可以提供所有隱藏字幕樣式參數，或稍後再設定。

   TVSDK會將隱藏字幕樣式資訊封裝在`TextFormat`介面中。 `TextFormatBuilder`類建立實現此介面的對象。

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

1. 要獲取對實現`TextFormat`介面的對象的引用，請調用`TextFormatBuilder.toTextFormat`公用方法。

   >[!NOTE]
   >
   >這會傳回可套用至媒體播放器的`TextFormat`物件。

   ```java
   public TextFormat toTextFormat()
   ```

1. （可選）執行下列任一操作，以取得目前的隱藏字幕樣式設定：

   * 獲取所有具有`MediaPlayer.getCCStyle`的樣式設定返回值是`TextFormat`介面的實例。

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * 透過`TextFormat`介面getter方法一次取得一個設定。

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

1. 要更改樣式設定，請執行下列操作之一：

   * 使用setter方法`MediaPlayer.setCCStyle` ，傳遞`TextFormat`介面的實例：

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

   * 使用`TextFormatBuilder`類別，它定義各個setter方法。

      `TextFormat`介面定義不可變對象，因此只有getter方法和無設定器。 您只能使用`TextFormatBuilder`類別來設定隱藏字幕樣式參數：

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
      >**色彩設定：** 在Android TVSDK 2.X中，已對隱藏字幕的色彩樣式進行增強。該增強功能允許使用表示RGB顏色值的十六進位字串來設定隱藏字幕顏色。 RGB十六進位色彩表示法是您在例如Photoshop等應用程式中使用的熟悉的6位元組字串：
      >
      >* FFFFFF =黑色
      >* 000000 =白色
      >* FF0000 =紅色
      >* 00FF00 =綠色
      >* 0000FF =藍色

      >
      >等等。
      >
      >在應用程式中，每當您將色彩樣式資訊傳遞至`TextFormatBuilder`時，您仍會像以前一樣使用`Color`列舉，但現在您必須將`getValue()`新增至色彩，才能將值當成字串。 例如：
      >
      >
      ```
      >tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      >```




設定隱藏字幕樣式是非同步操作，因此變更可能需要數秒鐘才會顯示在畫面上。

## 隱藏字幕樣式選項{#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

您可以指定數個標題樣式選項，而這些選項會覆寫原始標題中的樣式選項。

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
>在定義預設值的選項（例如`DEFAULT`）中，該值是指最初指定標題時的設定。

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
  <tr rowsep="1"> 
   <td colname="1"> 底部內嵌 </td> 
   <td colname="2"> <p>從標題視窗底部的垂直距離，以避免標題。 </p> <p>以字幕視窗高度（例如"20%"）或像素數（例如"20"）的百分比表示。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 安全區 </td> 
   <td colname="2"> <p>畫面邊緣的區域介於0%到25%之間，標題不會出現。 </p> <p>依預設，WebVTT的安全區域為0%。 此設定可讓您的應用程式覆寫該預設值。 如果提供兩個值，例如字串"10%,20%"，則第一個值是水準安全區，第二個值是垂直安全區。 如果提供一個值，例如字串"15%"，垂直軸和水準軸都使用指定的安全區域。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 標題格式示例{#section_58E8E82494EC4683B010FFDE67485CF9}

以下是一些範例，說明如何指定隱藏字幕格式。

**範例1:明確指定格式值**

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
