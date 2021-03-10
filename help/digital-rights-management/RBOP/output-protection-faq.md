---
description: 關於使用基於解析度的輸出保護的常見問題。
title: RBOP常見問答集
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# RBOP常見問答{#rbop-faq}

關於使用基於解析度的輸出保護的常見問題。

* **Q.** *當定義像素限制的數位輸出要求時，我在離開HDCP版本時會遇到剖析／格式錯誤，但我沒有任何HDCP要求。在這種情況下，我應如何設定數位輸出需求？* **A.** 由於HDCP版本檢查目前在客戶端中不受支援，Adobe建議將HDCP版本設定為 `1.0`。這將確保您的配置格式正確，並且在支援HDCP版本檢查時，在將來語義上保持一致。 以下程式碼片段說明使用此HDCP值的設定。

   ```
   { "pixelConstraints":  
     [  
       { "pixelCount": 720, "digital":  
         [  
           {  
             "output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}  
           }  
         ]  
       }  
     ]  
   }
   ```

* **Q. RBOP像** *素約束是離散的還是基於範圍的？* **A.** RBOP像素約束是基於區間的。每個像素計數定義所有像素計數的要求，這些像素計數小於或等於給定計數，或者如果存在多個像素約束，則最大計數小於該值。 簡而言之，這些值會套用為每個垂直像素計數的最大臨界值。

   假設垂直解析度為240、480、600、720和1080的MBR串流會透過下列RBOP設定傳遞給您的播放器。

   **RBOP策略設定：**

   * 720P —— 需要HDCP
   * 480P —— 無操作

   下列規則將套用至每個變數。

   **串流：**

   * 240, 480:兩者均&lt;= 480;不需要任何OP，而且不論有無HDCP，都會載入串流。
   * 600, 720:兩者均&lt;= 720;播放時需要HDCP
   * 一零八零年：> 720;由於上述規則中找不到串流，因此串流會列出區塊（傳回錯誤）。


* **問：在** 我的部分Android裝置上，我定義的像素計數限制並未完全套用定義。發生什麼了？

   **答：有** 些Android裝置報告的影格大小略高於一般大小。若要修正此情況，請將影格大小（`maxPixel`和`pixelCount`設定）向上調整20像素。 例如，從以下位置向上調整影格大小設定：

   ```
   { 
       "maxPixel": 800, 
       "pixelConstraints": [ 
           { "pixelCount": 532, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   至：

   ```
   { 
       "maxPixel": 820, 
       "pixelConstraints": [ 
           { "pixelCount": 552, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   遍及`maxPixel`和`pixelCount`的所有例項。

