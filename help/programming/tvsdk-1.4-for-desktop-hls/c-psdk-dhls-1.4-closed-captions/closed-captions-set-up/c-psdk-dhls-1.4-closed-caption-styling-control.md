---
description: 您可以使用ClosedCaptionStyles類別提供隱藏式字幕軌跡的樣式資訊。 這會設定播放器所顯示之任何隱藏式字幕的樣式。
title: 控制隱藏式字幕樣式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 控制隱藏式字幕樣式{#control-closed-caption-styling}

您可以使用ClosedCaptionStyles類別提供隱藏式字幕軌跡的樣式資訊。 這會設定播放器所顯示之任何隱藏式字幕的樣式。

此類別會封裝隱藏式字幕樣式資訊，例如字型型別、大小、顏色和背景不透明度。 關聯的協助程式類別， `ClosedCaptionStylesBuilder`，有助於使用隱藏式字幕樣式設定。

## 設定隱藏式字幕樣式 {#section_DAE84659D1964DB1B518F91B59AF29D9}

您可以使用TVSDK方法設定隱藏式字幕文字的樣式。

1. 等待MediaPlayer至少具有「已準備」狀態(請參閱 [等待有效的狀態](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md))。
1. 若要變更樣式設定，請執行下列任一項作業：

   * 使用 `ClosedCaptionStylesBuilder` 協助程式類別(操作於 `ClosedCaptionStyles` 幕後)。
   * 使用 `ClosedCaptionStyles` 直接分類。

>[!NOTE]
>
>設定隱藏式字幕樣式為非同步操作，因此可能需要幾秒鐘才會讓變更顯示在畫面上。

## 隱藏式字幕樣式選項 {#section_D28F50B98C0D48CF89C4FB6DC81C5185}

您可以使用為隱藏式字幕追蹤提供樣式資訊 `ClosedCaptionStyles` 類別。 這會設定播放器所顯示之任何隱藏式字幕的樣式。

```
public function TextFormat( 
   font:String = default,  
   size:String = default,  
   fontEdge:String = default,  
   fontColor:String = default,  
   backgroundColor:String = default,  
   fillColor:String = default,  
   edgeColor:String = default,  
   fontOpacity:int,  
   backgroundOpacity:int,  
   fillOpacity:int)
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
   <td colname="2"> <p>字型型別。 </p> <p>只能設定為以下定義的值： <span class="codeph"> ClosedCaptionStyles.FONT </span> 陣列，並代表有或沒有襯線的等寬。 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;AVCaptionStyle.MONOSPACE_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.MONOSPACED_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.CASUAL, 
      &nbsp;AVCaptionStyle.CURSIVE, 
      &nbsp;AVCaptionStyle.SMALL_CAPITALS 
      &nbsp;]; 
     </code> </p> <p>提示：裝置上可用的實際字型可能會有所不同，並會視需要使用替代。 通常使用含襯線的等寬做為替代字元，不過此替代字元可能是系統專屬的。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 大小 </td> 
   <td colname="2"> <p>註解的大小。 </p> <p> 只能設定為以下定義的值： <span class="codeph"> ClosedCaptionStyles.FONT_SIZE </span> 陣列： 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 中 </span>  — 標準大小 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 大 </span>  — 大約比中號大30% </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 小 </span>  — 大約比中型小30% </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> 預設 </span>  — 註解的預設大小；與「中」相同 </li> 
     </ul> </p> <p>提示：您可以變更WebVTT註解的字型大小，方法是 <span class="codeph"> DefaultMediaPlayer.ccStyles設定器 </span> 函式。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型邊緣 </td> 
   <td colname="2"> <p>用於字型邊緣的效果，例如凸出或無。 </p> <p>只能設定為以下定義的值： <span class="codeph"> ClosedCaptionStyles.FONT_EDGE </span> 陣列。 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT_EDGE&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.NONE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RAISED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEPRESSED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.UNIFORM, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.LEFT_DROP_SHADOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RIGHT_DROP_SHADOW 
      &nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字型顏色 </td> 
   <td colname="2"> <p>字型顏色。 </p> <p>只能設定為以下定義的值： <span class="codeph"> ClosedCaptionStyles.COLOR </span> 陣列。 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;COLOR&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLACK, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GRAY, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_CYAN&nbsp;&nbsp;&nbsp;]; 
     </code> </p> </td> 
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
   <td colname="2"> <p>文字所在視窗的背景色彩。 </p> <p>可設定為字型顏色可用的任何值。 </p> <p>重要：這不適用於WebVTT標題，因為WebVTT未使用此功能。 </p> </td> 
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

## 範例：註解格式 {#section_63E33840B7A14D26990046E2ACF2ECA1}

您可以指定隱藏式字幕格式。

## 範例1：明確指定格式值 {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    var formatBuilder:TextFormatBuilder = new TextFormatBuilder(); 
    formatBuilder.font = Font.DEFAULT,  
    formatBuilder.fontSize = FontSize.DEFAULT,  
    formatBuilder.fontEdge = FontEdge.DEFAULT,  
    formatBuilder.fontColor = Color.DEFAULT,  
    formatBuilder.backgroundColor = Color.DEFAULT,  
    formatBuilder.fillColor = Color.DEFAULT,  
    formatBuilder.edgeColor = Color.DEFAULT,  
    formatBuilder.fontOpacity = .DEFAULT_OPACITY,  
    formatBuilder.backgroundOpacity = Font.DEFAULT_OPACITY,  
    formatBuilder.fillOpacity = TextFormat.DEFAULT_OPACITY 
    mediaPlayer.set CCStyle(formatBuilder.toTextFormat()); 
} 
```

## 範例2：在引數中指定格式值 {#section_147036D7C31C4010A5A7DF49997014A9}

```
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param fontSize 
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
public function TextFormatBuilder(font:Font, fontSize:FontSize, fontEdge:FontEdge,  
                                  fontColor:Color, backgroundColor:Color,  
                                  fillColor:Color, edgeColor:Color, fontOpacity:int, 
                                  backgroundOpacity:int, fillOpacity:int); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public function toTextFormat():TextFormat; 
... 
```
