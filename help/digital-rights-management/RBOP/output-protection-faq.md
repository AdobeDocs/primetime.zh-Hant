---
description: 有關使用解析度型輸出保護的常見問題。
title: RBOP常見問題集
exl-id: 16b95db4-43a9-4458-b7f4-94033a36542e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# RBOP常見問題集 {#rbop-faq}

有關使用解析度型輸出保護的常見問題。

* **問：** *定義畫素限制的數位輸出需求時，我將HDCP版本保留在外時會收到剖析/格式設定錯誤，但我沒有任何HDCP需求。 在這種情況下，我該如何設定數位輸出需求？* **答：** 由於使用者端目前不支援HDCP版本檢查，Adobe建議將HDCP版本設定為 `1.0`. 這將確保您的設定格式正確，並在未來支援HDCP版本檢查時語意上一致。 以下程式碼片段說明具有此HDCP值的設定。

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

* **問：** *RBOP畫素限制是離散的還是以範圍為基礎？* **答：** RBOP畫素限制是以範圍為基礎。 每個畫素計數會定義小於或等於指定計數的所有畫素計數的需求，如果存在多個畫素限制，則最多會定義小於該值的最大計數。 簡而言之，這些值會套用為每個垂直畫素計數的最大臨界值。

   假設具有垂直解析度240、480、600、720和1080的MBR資料流透過下列RBOP設定傳遞給您的播放器。

   **RBOP原則設定：**

   * 720P — 需要HDCP
   * 480P — 無作業

   下列規則將套用至每個變體。

   **串流：**

   * 240、480：兩者皆小於= 480；不需要OP，而且無論是否有HDCP，資料流都會載入。
   * 600、720：都小於= 720；需要HDCP才能播放
   * 1080： > 720；資料流已列出區塊（傳回錯誤），因為在上述規則中找不到。


* **問：** 在我的一些Android裝置上，我定義的畫素計數限制並未完全依照定義套用。 發生什麼事了？

   **答：** 有些Android裝置報告的影格大小略高於正常大小。 若要補救這種情況，請調整影格大小( `maxPixel` 和 `pixelCount` 設定)向上20畫素。 例如，從下列位置向上調整影格大小設定：

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

   整個期間，適用於的所有執行個體 `maxPixel` 和 `pixelCount`.
