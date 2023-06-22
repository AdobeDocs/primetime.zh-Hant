---
description: 本節介紹配置範例，說明配置的概念和形式。
title: RBOP設定範例
exl-id: 0f40be83-9c7f-482b-ac42-9aa4e3f46f58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# RBOP設定範例 {#sample-rbop-configuration}

本節介紹配置範例，說明配置的概念和形式。

以下JSON設定範例會定義指定下列專案的畫素輸出原則：

* 將視訊解密限製為1080或以下的解析度
* 對720和480的解析度施加特定限制：

   * 720解析度：數位輸出需要HDCP；需要 *複製產生管理系統 — 類比* (CGMS-A)類比輸出的保護。
   * 480解析度：數位輸出需要HDCP；類比不需要保護

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

請注意上述範例設定的下列相關事項：

* 此 `pixelCount` 規格的JSON結構會向下調整一個層級，位於 `pixelConstraints` 區段。

* 在每個畫素計數規格中，數位和類比輸出均會指定輸出保護。
* 在數位輸出規格中，雖然使用者端目前不支援HDCP版本設定，但還是指定了HDCP版本。 如需詳細資訊，請參閱常見問題集。
