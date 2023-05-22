---
title: 如何使用黃金時段參考實現
description: 如何使用黃金時段參考實現
copied-description: true
exl-id: 45145f0d-c0e4-4d36-94fd-72f07619dc91
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 如何使用黃金時段參考實現 {#how-to-use-the-primetime-reference-implementation}

黃金時段參考實現是一個模組化播放器，已細分為各個功能，您可以通過專門的功能管理器輕鬆修改這些功能。 這些功能管理器用作連接應用程式和TVSDK庫的橋。

可通過以下方式使用參照實現：

* 按原樣使用，而不更改任何代碼（所有特徵都以預設值開啟）。
* 使用它作為參考，瞭解如何使用TVSDK庫。
* 通過關閉不使用的功能來選取應用於應用程式的功能。
* 定制UI元件，而不對功能進行任何更改。

我們提供黃金時段參考實現，幫助您瞭解TVSDK並輕鬆修改功能管理器以自定義您的播放器。 但是，請參閱 [《 TVSDK 1.4 for Android程式設計師指南》](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android.pdf) 的子菜單。

要方便地訪問Javadoc格式的參考實現API文檔，請按一下 [這裡](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/index.html)。
