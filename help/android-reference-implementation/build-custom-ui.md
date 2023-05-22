---
description: 您可以輕鬆構建基於參考實現框架的自定義用戶介面。
title: 構建自定義用戶介面
exl-id: 96008010-cd63-4fb1-a3fc-2fc94b624413
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 構建自定義用戶介面 {#build-a-custom-user-interface}

您可以基於參考實現框架構建自定義用戶介面。

以下功能的UI元件已整合：

* 可點擊的廣告
* 廣告覆蓋
* 延遲綁定音頻
* 隱藏字幕
* 上述所有元件的偵聽器

1. 編輯 [!DNL PlayerFragment.java] 檔案，以初始化要在播放器中使用的UI元件。

1. 編輯 [!DNL res/player/player_fragment.xml] 的子菜單。
1. 生成項目。

>[!NOTE]
>
>要對查找欄進行UI更改，可以編輯MarkableSeekBar類。 的 [可標籤搜索欄](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) 類處理滑塊、滑塊的拇指、標籤夾、提示標籤、緩衝區範圍和查找範圍背景。
