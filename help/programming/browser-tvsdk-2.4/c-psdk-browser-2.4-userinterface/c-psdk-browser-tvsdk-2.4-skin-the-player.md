---
description: 您可以使用以下資訊幫助您使玩家皮膚化。 對於每個可視結構，在預設行為中提到相應的行為。
title: 剝皮玩家
exl-id: 4ad50f96-d174-401f-a731-21e5fbfdbe31
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# 剝皮玩家 {#skinning-the-player}

您可以使用以下資訊幫助您使玩家皮膚化。 對於每個可視結構，在預設行為中提到相應的行為。

>[!IMPORTANT]
>
>此文檔中的外觀詳細資訊是UI框架建立的預設UI元素。 如果玩家修改了這些元素，則還需要更改外觀元素。

## 容器尺寸 {#section_99B0D598219D4150B57E97D5381B118F}

以下是容器窗口的樣式：

>[!TIP]
>
>這些DIV列在 `common-styles.css` 的子菜單。

以下是主div的樣式：

<table id="table_AC5745DF725543ADBBCD68BA6130DF12"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><b>主Div</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-main-video-div樣式</span> </td> 
   <td colname="col2"> <p>視頻播放的主div的樣式。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .pip模式活動</span> </td> 
   <td colname="col2"> <p>在PIP模式處於活動狀態時使用。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">預設行為是 <span class="codeph"> 視頻行為</span>。 </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>畫中畫(PIP)</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-pip-video-div</span> </td> 
   <td colname="col2"> <p>PIP視頻播放的div的樣式。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .view-as main-video</span> </td> 
   <td colname="col2"> <p>當初始PIP被交換並顯示為主視頻時，應用到它。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>多視頻視圖</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp — 多視圖容器</span> </td> 
   <td colname="col2"> <p>用於多視頻視圖。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp多視圖</span> </td> 
   <td colname="col2"> <p>放置在多視圖中每個視頻上的公用css樣式。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .多視圖</span> </td> 
   <td colname="col2"> <p>在多視圖中存放每個視頻的容器處於多視圖狀態時。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 各種控制項 {#section_E9E4A8E3AEBF4BDC89840B84B3B0E737}

下面是通用播放器控制項的樣式：

>[!TIP]
>
>這些樣式列在 `default-controls.css` 的子菜單。

<table id="table_0ACB6BAB5DAD42DBBD18CA7C0385A261"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp控制</span> </td> 
   <td colname="col2"> <p>適用於除洗滌器和空間外的控制欄上的所有控制項 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp輸入滑塊</span> </td> 
   <td colname="col2"> <p>輸入滑塊 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp面板標題</span> </td> 
   <td colname="col2"> <p>面板的標題 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-vertical-list-menu-item</span> </td> 
   <td colname="col2"> <p>垂直樣式的菜單清單 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp填充間隔物</span> </td> 
   <td colname="col2"> <p>控制欄上的空間 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-hr分隔符</span> </td> 
   <td colname="col2"> <p>水準規則分隔符 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-title</span> </td> 
   <td colname="col2"> <p>小組標題 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-close-btn</span> </td> 
   <td colname="col2"> <p>用於關閉面板的按鈕 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp按鈕背景</span> </td> 
   <td colname="col2"> <p>所有按鈕的背景 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-txt控制項</span> </td> 
   <td colname="col2"> <p>文本控制項的預設樣式。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 控制欄 {#section_B683B51EC746484B9AA90CB481D637BD}

以下是控制欄的樣式：

<table id="table_681E13F264674F849FAA2523EB65F094"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp控制欄</span> （預設行為）</td>
   <td colname="col2"> <p>適用於控制欄 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 功能按鈕 {#section_57FFD242FF674EA2867BCF6CA7F6B855}

>[!NOTE]
>
>下表中的字母與此圖中的字母相對應。

以下是搓衣板的樣式：

<table id="table_2207AD72E72A47FFA03AC748F06A54FD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式(A) </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar</span> </td> 
   <td colname="col2"> <p>控制欄上的擦洗欄 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-buffer-progress-bar</span> </td> 
   <td colname="col2"> <p>清除欄上的緩衝區進度欄 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-seek-to-bar</span> </td> 
   <td colname="col2"> <p>用戶正在查找擦洗欄時的狀態 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-playback-progress-bar</span> </td> 
   <td colname="col2"> <p>正常播放中清理欄的狀態 </p> </td> 
  </tr>
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-progress-bar-play-head</span> </td>
   <td colname="col2"> <p>在玩時在搓手板上玩頭 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-ad-marker-bar</span> </td>
   <td colname="col2"> <p>廣告標籤欄 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-ad標籤</span> </td>
   <td colname="col2"> <p>廣告標籤 </p> </td>
  </tr>
 </tbody>
</table>

預設行為為：

* `scrubBarBehavior`
* `bufferProgressBarBehavior`
* `playHeadBehavior`
* `playProgressBarBehavior`
* `seekToBarBehavior`

## 播放/暫停按鈕 {#section_F1F40A948D0049C5A4D8EA5F2A475CAA}

下面是播放/暫停按鈕的樣式：

<table id="table_975C2293222A4782A8C75A6149C1AD27">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式(B) </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn播放暫停</span> </td>
   <td colname="col2"> <p>在控制欄上播放暫停按鈕。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause狀態</span> </td>
   <td colname="col2"> <p><span class="codeph"> ptp-btn播放暫停</span> 暫停狀態 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause狀態</span> </td> 
   <td colname="col2"> <p><span class="codeph"> ptp-btn播放暫停</span> 在播放狀態 </p> </td>
  </tr>
 </tbody>
</table>

預設行為是 `playPauseButtonBehavior`。

## 卷 {#section_23E17BD2343948F8A2CEE1C8BEE2F874}

以下是配置卷按鈕的樣式：

<table id="table_8F9831F36A4D427CA31C9FFA4173170D">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式(C) </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><span class="codeph"> .ptp — 卷控制項</span>
     <ul id="ul_B12ADDFB83EA40FD8B4E92AF418AA4B4">
      <li id="li_7DA8143A69ED4E7D8A560B9FF75D6BA7"><span class="codeph"> 已擴展</span> </li>
      <li id="li_D8CCAD45D81C4850B6903FE261833AE6"><span class="codeph"> 垂直</span> </li>
     </ul> </p> </td>
   <td colname="col2"> <p>控制欄上的音量控制
     <ul id="ul_2C60F018FDCB458885738AC378C02F61">
      <li id="li_6B19572B504A4BBF9C97DC29C0E92A1D">當控制項為擴展形式時 </li>
      <li id="li_6489E422E1944D5194CBDFC8383D2F30">當控制項為垂直形式時 </li>
     </ul> </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn體積</span> </td>
   <td colname="col2"> <p>控制欄上的音量按鈕 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.min-volume-state</span> </td>
   <td colname="col2"> <p>當卷處於最小狀態時 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.mute狀態</span> </td>
   <td colname="col2"> <p>當卷處於靜音狀態時 </p> </td>
  </tr>
 </tbody>
</table>

預設行為為 `volumeBehavior` 和 `muteButtonBehavior`。

以下是卷滑塊的樣式：

<table id="table_E3DC93F8FC614C30AADAE259D18F10EF">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式(D) </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-volume-slider</span> </td>
   <td colname="col2"> <p>音量滑塊。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp — 卷隱藏</span> </td>
   <td colname="col2"> <p>處於隱藏狀態的卷滑塊。 </p> </td>
  </tr>
 </tbody>
</table>

預設行為是 `volumeSliderBehavior`。

## 倒帶 {#section_06EE608FC54A4CF5B5DF9DC743CFC740}

以下是倒帶按鈕的樣式：

<table id="table_0ACB116582D54B188E9F5B5C03D3A615">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式(E) </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>控制欄上的倒帶按鈕。 </p> </td>
  </tr>
 </tbody>
</table>

預設行為是 `rewindButtonBehavior`。

## 時間 {#section_0E6549B3DF6D4C10947D445A5F8EEA7F}

以下是在控制欄上顯示剩餘時間的樣式：

<table id="table_CEE62BFF5FB04FDCBBE1331E0D727EBA">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式(F) </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-txt顯示時間</span> </td>
   <td colname="col2"> <p>在控制欄上顯示剩餘時間 </p> </td>
  </tr>
</tbody>
</table>

預設行為是 `timeRemainingBehavior`。

## 快速倒帶 {#section_F6E6C65BD3BD493A89915DF9B92933BA}

下面是快速倒帶按鈕的樣式：

<table id="table_25BB4966B709402383AB6A6822FC1999">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式(G) </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>控制欄上的快速倒帶按鈕。 </p> </td>
  </tr>
 </tbody>
</table>

預設行為是 `fastRewindButtonBehavior`。

## 慢回風 {#section_38A22BB8681B430F8C6808C3BD21FB4E}

下面是慢迴旋按鈕的樣式：

<table id="table_E623C374622A497C91E22333D77AF8F6">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式(H) </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn慢速倒帶</span> </td>
   <td colname="col2"> <p>控制欄上的慢速後退按鈕。 </p> </td>
  </tr>
 </tbody>
</table>

預設行為是 `slowRewindButtonBehavior`。

## 慢進 {#section_92ACF092EECC4A5EAF6AA090C05E552E}

下面是慢進按鈕的樣式：

<table id="table_88C1CF5DB2D84EDBA01AC62B70509B08">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式(I) </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn慢進</span> </td>
   <td colname="col2"> <p>控制欄上的慢進按鈕。 </p> </td>
  </tr>
 </tbody>
</table>

預設行為是 `slowForwardButtonBehavior`。

## 快進 {#section_F90ED8B3739B49ACAB1F12DF18F0E4D6}

下面是快速前進按鈕的樣式：

<table id="table_F166BD1E8B934B34AF3690BBBAD894B7">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式(J) </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastforward</span> </td>
   <td colname="col2"> <p>控制欄上的快進按鈕。 </p> </td>
  </tr>
 </tbody>
</table>

預設行為是 `fastForwardButtonBehavior`。

## 音頻軌道 {#section_1CDF4FA5A1C14DB6B9C96579FFA1057C}

以下是配置音頻軌道的樣式：

<table id="table_22FC521D786B45EB84F230894FFECE79">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>音頻軌道按鈕(K)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-audio軌道</span> </td>
   <td colname="col2"> <p>控制欄上的音頻軌道按鈕。 </p> </td>
  </tr>
  <tr>
   <td colname="col1">預設行為是 <span class="codeph"> audioTrackButtonBehavior</span>。 </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>音頻軌道選擇面板(L)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection — 面板</span> </td> 
   <td colname="col2"> <p>用於選擇音頻軌道的面板。 </p> </td>
  </tr>
  <tr>
   <td colname="col1">預設行為是 <span class="codeph"> audioTrackSelectionPanelBehavior</span>。 </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>音頻軌道選擇標題(M)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>標題 <span class="codeph"> ptp-audio-track-selection面板</span>。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>音頻軌道選擇菜單(N)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-menu</span> </td>
   <td colname="col2"> <p>中的菜單項 <span class="codeph"> ptp-audio-track-selection面板</span>。 </p> </td>
  </tr>
 </tbody>
</table>

## 共用 {#section_B2ADC76E76304A68AD648A00A12B676E}

以下是配置共用的樣式：

<table id="table_3264C472809D462B8FC16680B96B1AC9">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式 </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>社交媒體共用按鈕(O)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video</span> </td> 
   <td colname="col2"> <p>將開啟的控制欄上的社交媒體共用按鈕 <span class="codeph"> ptp-share-video面板</span>。 </p> </td>
  </tr>
  <tr>
   <td colname="col1">預設行為是 <span class="codeph"> 共用VideoButtonBehavior</span>。 </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>共用視頻面板(P)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video面板</span> </td>
   <td colname="col2"> <p>顯示社交購股權的面板。 </p> </td>
  </tr>
  <tr>
   <td colname="col1">預設行為是 <span class="codeph"> 共用VideoPanelBehavior</span>。 </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>共用視頻菜單(Q)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>標題 <span class="codeph"> ptp-audio-track-selection面板</span>。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .share-video-panel菜單</span> </td>
   <td colname="col2"> <p>中的菜單 <span class="codeph"> ptp-share-video面板</span> 顯示在社交媒體上共用內容的所有選項。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video-panel-menu-item</span> </td>
   <td colname="col2"> <p>中的菜單項 <span class="codeph"> 共用視頻面板菜單</span>。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-facebook</span> </td>
   <td colname="col2"> <p>允許您在Facebook上共用內容的菜單項。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-twitter</span> </td>
   <td colname="col2"> <p>允許您在Twitter上共用內容的菜單項。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-google+</span> </td>
   <td colname="col2"> <p>允許您在GooglePlus上共用內容的菜單項。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-linkedin</span> </td>
   <td colname="col2"> <p>允許您在LinkedIn上共用內容的菜單項。 </p> </td>
  </tr>
 </tbody>
</table>

## 隱藏字幕 {#section_A01BA68218564DA0B7D6BF51F045D7AB}

以下是配置隱藏字幕的樣式：

<table id="table_777C7034C9424F8C841DABD480FFAC47">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 樣式 </th>
   <th colname="col2" class="entry"> 說明 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>隱藏字幕按鈕(R)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn — 閉標題</span> </td>
   <td colname="col2"> <p>的 <span class="uicontrol"> 隱藏字幕</span> 按鈕。 </p> </td>
  </tr>
  <tr>
   <td colname="col1">預設行為是 <span class="codeph"> closedCaptionButtonBehavior</span>。 </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .開狀態</span> </td>
   <td colname="col2"> <p>已為視頻啟用字幕。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>隱藏字幕面板(S)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp — 閉合字幕面板</span> </td>
   <td colname="col2"> <p>隱藏字幕面板。 </p> </td>
  </tr>
  <tr>
   <td colname="col1">預設行為是 <span class="codeph"> closedCaptionLanguagePanelBehavior</span>。 </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>隱藏字幕語言(T)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-close-caption-language-panel:</span> </td>
   <td colname="col2"> <p>標題 <span class="codeph"> ptp-audio-track-selection面板</span>。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-close-caption-language-menu: </span> </td>
   <td colname="col2"> <p>隱藏字幕面板中的菜單。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>隱藏字幕選項(U)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp — 閉合標題 — 選項 — btn</span> </td>
   <td colname="col2"> <p>的 <span class="uicontrol"> 選項</span> 按鈕。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp — 閉合字幕 — 選項 — 面板</span> </td>
   <td colname="col2"> <p>隱藏字幕面板上的「選項」面板。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-close-caption-menu-item</span> </td>
   <td colname="col2"> <p>隱藏字幕面板中的菜單項。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> 已選定</span> </td>
   <td colname="col2"> <p>處於選定狀態。 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp — 閉合標題 — 完成 — btn</span> </td> 
   <td colname="col2"> <p>的 <span class="uicontrol"> 完成</span> 按鈕。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp — 閉合字幕 — 選項 — 菜單</span> </td> 
   <td colname="col2"> <p>隱藏字幕中的「選項」菜單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-close-caption-options-main菜單</span> </td> 
   <td colname="col2"> <p>隱藏標題選項的主菜單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-close-caption-options-sub菜單</span> </td> 
   <td colname="col2"> <p>隱藏標題選項的子菜單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options — 不透明度滑塊</span> </td> 
   <td colname="col2"> <p>隱藏字幕選項的不透明度滑塊。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-close-caption-options-menu-sepator</span> </td> 
   <td colname="col2"> <p>隱藏標題選項分隔符。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-close-caption-options-menu-item</span> </td> 
   <td colname="col2"> <p>隱藏標題 <span class="uicontrol"> 選項</span> 的子菜單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-close-caption-preview — 面板</span> </td> 
   <td colname="col2"> <p>隱藏字幕預覽面板。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-close-caption-options-footer</span> </td> 
   <td colname="col2"> <p>隱藏標題選項頁腳。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-close-caption-options-reset-button</span> </td> 
   <td colname="col2"> <p>的 <span class="uicontrol"> 重置</span> 按鈕。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-apply-button</span> </td> 
   <td colname="col2"> <p>的 <span class="uicontrol"> 應用</span> 按鈕。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">預設行為是 <span class="codeph"> closedCaptionOptionsPanelBehavior</span>。 </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## 更多選項(V) {#section_18E25CF8A8964FFD9026A8A833089CE3}

以下是配置其他選項的樣式：
<table id="table_EC6EF88E2EDE4B8EBB1C14F87A6161FA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more選項</span> </td> 
   <td colname="col2"> <p>的 <span class="uicontrol"> 更多選項</span> 按鈕 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more選項.ptp-control-bar-btn</span> </td> 
   <td colname="col2"> <p>的 <span class="codeph"> ptp-btn-more選項</span> 控制項欄中的。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel</span> </td> 
   <td colname="col2"> <p>「更多選項」控制面板。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu</span> </td> 
   <td colname="col2"> <p>「更多選項」控制面板菜單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu-item</span> </td> 
   <td colname="col2"> <p>「更多選項」控制面板菜單項。 </p> </td> 
  </tr> 
 </tbody> 
</table>

預設行為是 `moreOptionsButtonBehavior`。

## PIP按鈕(W) {#section_1EE039DEA99541D391B30BD1DF72A83E}

這是 [!UICONTROL PIP<] 按鈕：

<table id="table_EE2E882C87E24D39B8D5347686F29E55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-pip</span> </td> 
   <td colname="col2"> <p>控制欄上的PIP按鈕。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">預設行為是 <span class="codeph"> pipButtonBehavior</span>。 </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## 全屏(X) {#section_158A19DFB30E4432A67E4A74A7CBA563}

以下是配置全屏的樣式：

<table id="table_5941835F31AC4E9CBA9702AB8D813B8F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn全屏</span> </td> 
   <td colname="col2"> <p>的 <span class="uicontrol"> 全屏</span> 按鈕。 </p> </td> 
  </tr> 
 </tbody> 
</table>

預設行為是 `fullScreenButtonBehavior`。

## 特技遊戲(Y) {#section_AE6F83BB7EE2497FB13CD94A8316192D}

以下是配置特技播放的樣式：

<table id="table_F1ADAC0A4B4E48669828690BDEB4BC09"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-control-bar-tric-play rate(.ptp-control-bar-tric-play-play-rate)</span> </td> 
   <td colname="col2"> <p>控制欄中的特技率顯示元件。 </p> </td> 
  </tr> 
 </tbody> 
</table>

預設行為是 `trickPlayRateDisplayBehavior`。

## 多視圖(Z) {#section_58EFAE7263BA45D3A4E2AB7309A9CAA7}

以下是配置多視圖的樣式：

<table id="table_84B37D7410EE40DFA7A8BB8431C6DCF0"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn多視圖</span> </td> 
   <td colname="col2"> <p>的 <span class="uicontrol"> 多視圖</span> 按鈕，以及 <span class="uicontrol"> 多視圖</span> 按鈕 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">預設行為是 <span class="codeph"> multiViewButtonBehavior</span>。 </td> 
   <td colname="col2"> </td> 
  </tr> 
 </tbody> 
</table>

## 縮略圖 {#section_0AFD932975634BB08387EEE7D3BFC438}

以下是配置縮略圖的樣式：

<table id="table_968136A8BBA042A7A8E79739B8F92F55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-progress-bar-thumb-nail</span> </td> 
   <td colname="col2"> <p>縮略圖的進度欄。 </p> </td> 
  </tr> 
 </tbody> 
</table>

預設預設行為是 `thumbnailPreviewBehavior`。

## 錯誤消息 {#section_AC9858EE1B5A4FF4947E383C663B6AB5}

以下是配置錯誤消息的樣式：

<table id="table_7F4C156170DB4AFFA7DEE06F00449506"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel</span> </td> 
   <td colname="col2"> <p>顯示播放器錯誤消息的面板。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-icon</span> </td> 
   <td colname="col2"> <p>出現錯誤消息時顯示在面板上的表徵圖。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-message</span> </td> 
   <td colname="col2"> <p>顯示的錯誤消息。 </p> </td> 
  </tr> 
 </tbody> 
</table>

預設行為是 `errorMessagePanelBehavior`。

## 緩衝覆蓋 {#section_2FE8FDE2599E42BAA7411D0D38FA0A88}

以下是配置縮略圖的樣式：

<table id="table_1FECE1DC29B8434B886751A29455F004"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp緩衝覆蓋</span> </td> 
   <td colname="col2"> <p>緩衝覆蓋控制項。 </p> </td> 
  </tr> 
 </tbody> 
</table>

預設覆蓋為 `bufferingOverlayBehavior`。

## 特定選擇器 {#section_51F735AEF82E41E890FF59E031A0DB89}

下面是快速前進按鈕的樣式：

<table id="table_E77EDC7D227348E79C7E73FB5D46F992"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 樣式 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ad break</span> </td> 
   <td colname="col2"> <p>播放廣告時控制面板的狀態。 </p> <p>適用於以下項： 
     <ul id="ul_D5076303DCD94D968682289823D1A9F2"> 
      <li id="li_4290C4B2D48546E3AD023BED6CAAE395"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_72A3D3E916E44A55BA170407EAB0527D"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_A0BAEBB0E01B402EB83E3CE9B92B15CC"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_FDF2CEDB0A854098907FF9CBCF1A61C1"><span class="codeph"> .ptp-btn慢進</span> </li> 
      <li id="li_CD2E14DB3DD64C10A253DA23FBE04A04"><span class="codeph"> .ptp-btn慢進</span> </li> 
      <li id="li_A230359E8F7F4571A9EBFF0E4C2462D7"><span class="codeph"> .ptp-btn慢速倒帶</span> </li> 
      <li id="li_5711A315872F4FA59FDDF0EF0AFD03C6"><span class="codeph"> .ptp-btn-more選項 </span> </li> 
      <li id="li_71C8E76077A84ED590160AB5ABFCC0D7"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_4A3113C0360F4F708AAA96AB316FA057"><span class="codeph"> .ptp-btn — 閉標題 </span> </li> 
      <li id="li_901A0186D65A48A1B774DC555CEC5367"><span class="codeph"> .ptp-btn-audio軌道</span> </li> 
      <li id="li_2331583C01C2482B8EE72979FBF111DB"><span class="codeph"> .ptp-btn-pip </span> </li> 
      <li id="li_7BB39BDF5E294AEB8FA3DCD9F9A29468"><span class="codeph"> .ptp-btn倒帶</span> </li> 
      <li id="li_E4FEF5A7486A40F6A5FE1119BD63AFEF"><span class="codeph"> .ptp-scrub-bar</span> </li> 
      <li id="li_12153547558A4871842EE0416BCCA8B2"><span class="codeph"> .ptp-seek-to-bar</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .多視圖</span> </td> 
   <td colname="col2"> <p>在多視圖中時控制項的狀態。 </p> <p>適用於以下項： 
     <ul id="ul_A8AC653C30814AC49041F3B58A2106F4"> 
      <li id="li_0407167DA21647A8A6960DFE55A33F42"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_EA71CAF41CDC41DE859A85CE482BE97C"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_F3A998C51A034C22A914EAEFF19FFEA7"><span class="codeph"> .ptp-btn — 閉標題</span> </li> 
      <li id="li_022F871ABC894C9BA879B3AF3D341202"><span class="codeph"> .ptp-btn-audio軌道</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .全屏狀態</span> </td> 
   <td colname="col2"> <p>播放器處於全屏模式。 </p> <p>適用於以下項： 
     <ul id="ul_B235C1D339F64B2FAC6BC72F03807616"> 
      <li id="li_6E050EE74C604FDAB4C9C0447F547A9D"><span class="codeph"> .ptp控制項欄 </span> </li> 
      <li id="li_67D54B1A41764B2DA544479CDA1C901C"><span class="codeph"> .ptp-btn全屏</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
