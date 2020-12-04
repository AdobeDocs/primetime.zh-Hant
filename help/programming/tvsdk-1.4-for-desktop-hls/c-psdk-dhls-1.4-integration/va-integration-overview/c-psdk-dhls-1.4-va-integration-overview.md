---
description: 您可以透過整合TVSDK與Adobe Analytics來追蹤視訊的使用。
seo-description: 您可以透過整合TVSDK與Adobe Analytics來追蹤視訊的使用。
seo-title: 視訊分析
title: 視訊分析
uuid: c3cb0574-1117-409c-8aa7-641363d8d85f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# 視訊分析{#video-analytics}

您可以透過整合TVSDK與Adobe Analytics來追蹤視訊的使用。

TVSDK中的視訊追蹤使用&#x200B;**Adobe Analytics Video Essentials**&#x200B;服務，提供視訊參與度量，例如視訊檢視、視訊完成、廣告印象、視訊逗留時間等。 如需此服務的詳細資訊，請連絡您的Adobe代表。

下列程式會摘要啟動播放器中視訊追蹤的步驟：

1. 初始化及／或設定下列視訊追蹤元件：

   * **AppMeasurement程式庫** -包含低階資料收集核心邏輯。這是透過網路累積和傳送視訊心率資料的地方。
   * **視訊心率程式庫** -包含視訊心率資料收集核心邏輯。視訊心率程式庫可存取`AppMeasurement`程式庫API的子集。

      >[!TIP]
      >
      >您的應用程式不會直接與視訊心率程式碼互動。 應用程式會改用TVSDK API來設定您播放器的視訊追蹤功能。

   * **VisitorID Library**  —— 唯一識別代管視訊播放器之網頁的訪客。
   >[!IMPORTANT]
   >
   >TVSDK內建視訊追蹤功能取決於正確設定的`AppMeasurement`例項。 追蹤元素假設在設定和啟動視訊追蹤之前，`AppMeasurement`程式庫已執行個體化並設定。 TVSDK視訊追蹤功能取決於`AppMeasurement`程式庫是否有完整功能且已正確設定的例項。

1. 使用Adobe Analytics管理工具在伺服器端設定視訊分析報表。

