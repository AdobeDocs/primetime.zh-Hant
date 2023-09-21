---
description: 您可以根據參考實作架構輕鬆建置自訂使用者介面。
title: 建置自訂使用者介面
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 建置自訂使用者介面 {#build-a-custom-user-interface}

您可以根據參考實作框架建置自訂使用者介面。

下列功能的UI元件已整合：

* 可點按的廣告
* 廣告覆蓋
* 延遲繫結音訊
* 隱藏式字幕
* 上述所有元件的接聽程式

1. 編輯 [!DNL PlayerFragment.java] 檔案來初始化您要在播放器中使用的UI元件。

1. 編輯 [!DNL res/player/player_fragment.xml] 檔案來自訂使用者介面。
1. 建立專案。

>[!NOTE]
>
>若要變更搜尋列的UI，您可以編輯MarkableSeekBar類別。 此 [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) class會處理滑桿、滑桿的thumb、廣告標籤保持器、提示標籤、緩衝範圍和搜尋範圍背景。
