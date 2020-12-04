---
description: 本節介紹了一個示例配置，其中說明了配置的概念和形式。
seo-description: 本節介紹了一個示例配置，其中說明了配置的概念和形式。
seo-title: RBOP配置示例
title: RBOP配置示例
uuid: fa5ead93-36c5-4ad1-947b-c4f1f2632d9b
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# RBOP配置示例{#sample-rbop-configuration}

本節介紹了一個示例配置，其中說明了配置的概念和形式。

下列範例JSON設定定義像素輸出原則，指定下列項目：

* 將視訊解密限制為1080或以下解析度
* 對第720和480號決議施加具體限制：

   * 針對720項決議：需要HDCP才能進行數位輸出；需要&#x200B;*複製生成管理系統——模擬*(CGMS-A)保護才能輸出模擬。
   * 針對480項決議：需要HDCP才能進行數位輸出；不需要模擬保護

```
{ 
  "pixelConstraints":  
    [ 
      { 
        "pixelCount": 720, 
        "digital": 
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "REQUIRED_CGMSA"} 
      }, 
      { 
        "pixelCount": 480, 
        "digital":  
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "NO_PROTECTION"} 
      } 
    ], 
  "maxPixel": 1080 
}
```

請注意上述範例組態的下列相關資訊：

* `pixelCount`規格在JSON結構中為下一層，位於`pixelConstraints`區段中。

* 在每個像素計數規範中，為數字和模擬輸出指定輸出保護。
* 在數位輸出規格中，雖然用戶端目前不支援HDCP版本控制，但是會指定HDCP版本。 如需詳細資訊，請參閱常見問答集。

