---
description: 您可以輕鬆建立以參考實施架構為基礎的自訂使用者介面。
seo-description: 您可以輕鬆建立以參考實施架構為基礎的自訂使用者介面。
seo-title: 建立自訂使用者介面
title: 建立自訂使用者介面
uuid: b785f6a4-3ef8-4f7a-a087-0d6551da9750
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 建立自訂使用者介面 {#build-a-custom-user-interface}

您可以根據參考實作架構建立自訂的使用者介面。

下列功能的UI元件已整合：

* 可點選廣告
* 廣告覆蓋
* 延遲裝訂音訊
* 隱藏字幕
* 以上所有元件的監聽程式

1. 編輯 [!DNL PlayerFragment.java] 檔案以初始化您要在播放器中使用的UI元件。

1. 編輯檔 [!DNL res/player/player_fragment.xml] 案以自訂使用者介面。
1. 建立專案。

>[!NOTE]
>
>若要變更搜尋列的UI，您可以編輯MarkableSeekBar類別。 MarkableSeekBar [](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) 類別可處理滑桿、滑桿的拇指、廣告標籤夾持器、提示標籤、緩衝範圍和搜尋範圍背景。