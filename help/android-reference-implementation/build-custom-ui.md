---
description: 您可以根據參考實作架構輕鬆建置自訂使用者介面。
title: 建立自訂使用者介面
exl-id: 96008010-cd63-4fb1-a3fc-2fc94b624413
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 建立自訂使用者介面 {#build-a-custom-user-interface}

您可以根據參考實作架構來建置自訂使用者介面。

已整合下列功能的UI元件：

* 可點按的廣告
* 廣告覆蓋圖
* 延遲繫結音訊
* 隱藏式字幕
* 上述所有元件的監聽器

1. 編輯 [!DNL PlayerFragment.java] 檔案來初始化您要在播放器中使用的UI元件。

1. 編輯 [!DNL res/player/player_fragment.xml] 檔案來自訂使用者介面。
1. 建立專案。

>[!NOTE]
>
>若要對搜尋列進行UI變更，您可以編輯MarkableSeekBar類別。 此 [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) class會處理滑桿、滑桿縮圖、廣告標籤保留區、提示標籤、緩衝範圍和搜尋範圍背景。
