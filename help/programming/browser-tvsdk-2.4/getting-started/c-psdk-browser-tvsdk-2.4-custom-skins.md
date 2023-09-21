---
description: 若要使用自訂外觀元素，您必須撰寫類似於default-video-controls.css的自訂專案，並在播放器中參照此新自訂專案。
title: 自訂外觀元素
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 自訂外觀元素{#custom-skins}

若要使用自訂外觀元素，您必須撰寫類似於default-video-controls.css的自訂專案，並在播放器中參照此新自訂專案。

例如，您可以使用下列其中一個選項：

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

您可以進行下列型別的變更：

* 按鈕和文字的前景色彩

  所有具有前景的控制項都使用 `vid-skin-fgcolor` 類別。 若要變更所有控制項的前景，請以 `vid-skin-fgcolor` 類別並指定所要的顏色。
* 按鈕和文字的背景顏色

  所有具有前景的控制項都使用 `vid-skin-bgcolor` 類別。 若要變更所有控制項的前景，請透過以下方式逐一檢視所有元素 `vid-skin-bgcolor` 類別並指定所要的顏色。
* 播放點形狀

  播放磁頭可以是方形或圓形。 若要變更播放點，請新增 `square` 或 `round` 類別至 `playhead` 元素。
* 緩衝迴轉器的樣式

  參考播放器提供下列的迴轉器樣式，可在播放器緩衝內容時顯示：

   * 覆蓋文字( `overlay-text`)
   * 矩形旋轉圖示( `spinner`)
   * 訊號( `signal`)
   * 垂直條( `vertical`)

     >[!TIP]
     >
     >若要使用任何緩衝旋轉器，您必須在緩衝覆蓋元素中新增類別。 例如，若要使用 `overlay-text`，在中新增下列行 `BufferOverlay.js` 檔案：
     >
     >```js
     >var overlay = document.getElementById("buffering-overlay"); 
     >overlay.classList.add ("spinner");
     >```
     >
