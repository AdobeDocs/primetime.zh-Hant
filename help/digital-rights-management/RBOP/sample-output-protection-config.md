---
description: 本節提供了一個示例配置，它說明了配置的概念和形式。
title: 示例RBOP配置
exl-id: 0f40be83-9c7f-482b-ac42-9aa4e3f46f58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 示例RBOP配置 {#sample-rbop-configuration}

本節提供了一個示例配置，它說明了配置的概念和形式。

以下示例JSON配置定義了指定以下項的像素輸出策略：

* 將視頻解密限制為1080或更低解析度
* 對第720和480號決議施加具體限制：

   * 720號決議：需要HDCP進行數字輸出；要求 *複製生成管理系統 — 模擬* (CGMS-A)模擬輸出保護。
   * 480項決議：需要HDCP進行數字輸出；不需要模擬保護

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

請注意上述示例配置的以下內容：

* 的 `pixelCount` 規範在JSON結構中是向下一級，在 `pixelConstraints` 的子菜單。

* 在每個像素計數規範內，為數字和模擬輸出都指定輸出保護。
* 在數字輸出規範中，指定了HDCP版本，儘管客戶端當前不支援HDCP版本控制。 有關詳細資訊，請參閱常見問題解答。
