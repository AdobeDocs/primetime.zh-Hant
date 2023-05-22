---
description: 有關使用基於解析度的輸出保護的常見問題。
title: RBOP常見問題
exl-id: 16b95db4-43a9-4458-b7f4-94033a36542e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# RBOP常見問題 {#rbop-faq}

有關使用基於解析度的輸出保護的常見問題。

* **問：** *在定義像素約束的數字輸出要求時，當我將HDCP版本保留在外時，我會遇到解析/格式化錯誤，但我沒有任何HDCP要求。 在這種情況下，我應如何配置數字輸出要求？* **答：** 由於客戶端當前不支援HDCP版本檢查，Adobe建議將HDCP版本設定為 `1.0`。 這將確保配置格式正確，並且在支援HDCP版本檢查時在語義上保持一致。 以下代碼段說明了具有此HDCP值的配置。

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

* **問：** *RBOP像素約束是離散的還是基於範圍的？* **答：** 基於RBOP像素約束進行排序。 每個像素計數定義了對於小於或等於給定計數的所有像素計數的要求，或者如果存在多個像素約束，則定義對小於該值的最大計數的要求。 簡言之，這些值應用為每個垂直像素計數的最大閾值。

   假設垂直解析度為240、480、600、720和1080的MBR流通過以下RBOP設定傳遞給您的播放器。

   **RBOP策略設定：**

   * 720P — 需要HDCP
   * 480P — 無操作

   以下規則將應用於每個變型。

   **流：**

   * 240、480:兩者均&lt;= 480;不需要OP，流將載入HDCP或不提供HDCP。
   * 600、720:兩者均&lt;= 720;播放需要HDCP
   * 1080:> 720;流列出了塊（返回錯誤），因為在上述規則中找不到它。


* **問：** 在我的一些Android設備上，我定義的像素計數限制沒有完全按照定義應用。 怎麼了？

   **答：** 一些Android設備報告的幀大小略高於正常大小。 要糾正此情況，請調整幀大小( `maxPixel` 和 `pixelCount` 設定)向上20像素。 例如，從以下位置向上調整幀大小設定：

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

   整個，對於所有實例 `maxPixel` 和 `pixelCount`。
