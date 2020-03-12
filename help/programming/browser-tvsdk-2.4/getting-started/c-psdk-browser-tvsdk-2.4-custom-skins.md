---
description: 若要使用自訂外觀，您必須編寫類似default-video-controls.css的自訂內容，並參閱播放器中的這項新自訂內容。
seo-description: 若要使用自訂外觀，您必須編寫類似default-video-controls.css的自訂內容，並參閱播放器中的這項新自訂內容。
seo-title: 自訂外觀
title: 自訂外觀
uuid: bc71926e-0dec-4628-8248-911224a7a6c2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 自訂外觀{#custom-skins}

若要使用自訂外觀，您必須編寫類似default-video-controls.css的自訂內容，並參閱播放器中的這項新自訂內容。

例如，您可使用下列其中一個選項：

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

您可進行下列類型的變更：

* 按鈕和文字的前景色

   所有具有前景的控制項都使用 `vid-skin-fgcolor` 類別。 若要變更所有控制項的前景，請循環使用類別的所有元素， `vid-skin-fgcolor` 並指定所要的顏色。
* 按鈕和文字的背景顏色

   所有具有前景的控制項都使用 `vid-skin-bgcolor` 類別。 若要變更所有控制項的前景，請循環使用類別的所有元素， `vid-skin-bgcolor` 並指定所要的顏色。
* 遊戲頭的形狀

   播放頭可以是正方形或圓形。 若要變更播放頭，請新增 `square` 或 `round` 類別至 `playhead` 元素。
* 緩衝旋壓器的樣式

   參考播放器提供下列旋轉器的樣式，可顯示為播放器緩衝內容：

   * 覆蓋文字( `overlay-text`)
   * 矩形微調按鈕( `spinner`)
   * 信號( `signal`)
   * 垂直條( `vertical`)

      >[!TIP]
      >
      >若要使用任何緩衝旋轉器，您必須在緩衝覆蓋元素中新增類別。 例如，若要使用 `overlay-text`，請在檔案中新增下列 `BufferOverlay.js` 行：      >
      >
      >
      ```js      >
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```      >
      >



