---
description: 要使用自定義外觀，必須編寫類似於default-video-controls.css的自定義項，並在播放器中引用此新自定義項。
title: 自定義外觀
exl-id: 4d627545-942d-4883-a010-afddcffb8dd5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 自定義外觀{#custom-skins}

要使用自定義外觀，必須編寫類似於default-video-controls.css的自定義項，並在播放器中引用此新自定義項。

例如，可以使用以下選項之一：

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

可以進行以下類型的更改：

* 按鈕和文本的前景色

   具有前景的所有控制項都使用 `vid-skin-fgcolor` 類。 要更改所有控制項的前景，請使用 `vid-skin-fgcolor` 類並指定所需顏色。
* 按鈕和文本的背景顏色

   具有前景的所有控制項都使用 `vid-skin-bgcolor` 類。 要更改所有控制項的前景，請循環訪問所有元素 `vid-skin-bgcolor` 類並指定所需顏色。
* 遊戲頭的形狀

   播放頭可以是方形的或圓形的。 要更改播放頭，請添加 `square` 或 `round` 類 `playhead` 的子菜單。
* 緩衝旋壓器的樣式

   所述參考播放器提供以下旋轉器樣式，可以作為播放器緩衝內容顯示：

   * 覆蓋文本( `overlay-text`)
   * 矩形旋轉器( `spinner`)
   * 信號( `signal`)
   * 竪條( `vertical`)

      >[!TIP]
      >
      >要使用任何緩衝旋轉器，必須在buffering-overlay元素中添加類。 例如，要使用 `overlay-text`，在 `BufferOverlay.js` 檔案：
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```
